# Transformers

## Self-attention with queries, keys and values

Status: **Can explain** the roles of Q, K and V and how softmax weights depend on the other tiles.

- **Meaning** — Each tile embedding is projected into a query, a key and a value. A tile's query is scored against the available keys. Softmax converts those scores into weights that sum to one for that query. The attention output is the weighted sum of the value vectors. Reversing the direction swaps which tile supplies the query and the key, so the weights can differ.
- **Uses** — Update a tile embedding using the other tiles as context. A transformer can serve as the aggregator in a whole-slide MIL model.
- **Pitfalls** — Equal scores yield the mean of the projected values for that query and head. Every finite, unmasked score contributes to the softmax denominator after exponentiation. With the original scores fixed, adding tiles lowers a tile's weight even if it still ranks first. Crop and whole-slide attention weights therefore depend on which keys are available.
- **Methods** — Transformer self-attention and transformer aggregation in multiple instance learning (MIL).

## Testing spatial context in whole-slide attention

Status: **Can apply** to a hypothetical experiment.

- **Meaning** — Attention can use the other tiles as context. Coordinates or another source of positional information let it also use physical arrangement.
- **Uses** — Test whether the true tile arrangement improves prediction while holding each slide's tissue content fixed.
- **Pitfalls** — A gain from real coordinates establishes predictive value under the comparison. Identifying the specific biological pattern requires a separate test.
- **Methods** — Shuffle the pairing between tile embeddings and coordinates within each slide. Train and evaluate with true versus shuffled coordinates using the same patient splits. Shuffling only at test time measures sensitivity to that disruption.

## Attention matrices and local attention

Status — **Can explain** the difference between pairwise scores and per-tile outputs, and how information travels through local attention layers.

- **Meaning** — Start with the score matrix. Row `i` contains the scores for tile `i` attending to the available tiles. Q and K compute the scores. Row-wise softmax turns them into weights, and the weighted sum of the V vectors gives one output vector per row. With 2,000 tiles and 64 features per value vector, one head has a 2,000 × 2,000 score matrix and a 2,000 × 64 output. Doubling the tile count quadruples the full pairwise score count and doubles the number of output vectors.
- **Uses** — Local attention limits each row to nearby tiles. Allowing 64 keys per tile gives up to 128,000 scores for 2,000 tiles, compared with 4 million for full attention.
- **Pitfalls** — With fixed adjacency, each layer recomputes scores for the same allowed pairs using updated vectors. Information can travel one more hop per layer along those connections. If the same non-overlapping windows are used at every layer, information stays within each window.
- **Methods** — Shift the windows between layers to let information cross the original boundaries. Hierarchical pooling can also connect windows when coarser groups span those boundaries.

**Retrieval question** — If the tile count doubles, how do the number of full-attention scores and the number of output vectors change?

**Resume** — Use the score matrix to compare what full attention, shifted windows and hierarchical pooling can capture on a whole slide.

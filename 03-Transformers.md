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

**Retrieval question** — Why can a tile retain the highest score yet receive less attention when more tiles are added?

**Resume** — Follow one attention head through the shapes of Q, K, V and the score matrix, then connect that to why full attention can be expensive on whole slides.

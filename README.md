# Character-level-recurrent-sequence-to-sequence-model
It demonstrates the implementation of a basic character-level recurrent sequence-to-sequence model

Here, I'm translating short English sentences into short French sentences, character-by-character.

Starting with the input sequences from a domain (e.g. English sentences) and corresponding target sequences from another domain (e.g. French sentences).

An encoder LSTM turns input sequences to 2 state vectors (keeping the last LSTM state and discarding the outputs).

A decoder LSTM is trained to turn the target sequences into the same sequence but offset by one timestep in the future, a training process called "teacher forcing" in this context. It uses as initial state the state vectors from the encoder. Effectively, the decoder learns to generate targets[t+1...] given targets[...t], conditioned on the input sequence.

In inference mode, after decoding unknown input sequences,
- Encoded the input sequence into state vectors - Started with a target sequence of size 1 (just the start-of-sequence character) - Feeding the state vectors and 1-char target sequence to the decoder to produce predictions for the next character - Sampling the next character using these predictions (simply used argmax). - Appending the sampled character to the target sequence - Repeated these until the end-of-sequence character gets generated or it hit the character limit.

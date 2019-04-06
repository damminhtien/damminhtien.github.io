A blockchain is an *immutable*, *sequential* chain of records called Blocks. They can contain transactions, files or any data you like, really. But the important thing is that they’re chained together using *hashes*.

Each new block contains within itself, the hash of the previous Block. This is crucial because it’s what gives blockchains immutability: If an attacker corrupted an earlier Block in the chain then all subsequent blocks will contain incorrect hashes.

When Blockchain is instantiated we’ll need to seed it with a genesis block—a block with no predecessors. We’ll also need to add a “proof” to our genesis block which is the result of mining (or proof of work).
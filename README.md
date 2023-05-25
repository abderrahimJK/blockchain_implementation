# Blockchain Workshop


This project is a simple implementation of a blockchain using Java. The blockchain is a decentralized, distributed ledger that is used to record transactions across many computers.
Each block in the chain contains a cryptographic hash of the previous block, a timestamp, and transaction data.

# How it Works
The blockchain is implemented using a simple Block class that contains :

 - the block's hash
 - previous hash
 - timestamp
 - transactions
 - data.

The `Blockchain` class is responsible for adding new blocks to the chain and verifying the integrity of the chain.
When a new block is added to the chain, the Blockchain class first checks to make sure that the previous block's hash matches the current block's previous hash.
If the hashes match, the new block is added to the chain. If the hashes do not match, the block is rejected.

- adding new block

```java
public Block addBlock(Block block) {
        if (isValidBlock(block)) {
            chain.add(block);
            transactionPool.removeTransactions(block.getTransactions());
            return block;
        }
        throw new InvalidParameterException();
}
```
- validate Block:

```java
public boolean isValidBlock(Block block) {
        Block previousBlock = getLatestBlock();

        // Check if the index is incrementing by 1
        if (block.getIndex() != previousBlock.getIndex() + 1) {
            return false;
        }

        // Check if the previous hash matches
        if (!block.getPreviousHash().equals(previousBlock.getCurrentHash())) {
            return false;
        }

        // Check if the block hash meets the difficulty requirement
        String prefix = getDifficultyPrefix(difficulty);
        return block.getCurrentHash().startsWith(prefix);

}
```

The Blockchain class also includes a `mineBlock()` method that simulates the process of mining a block. In a real blockchain, mining involves solving a complex mathematical problem to add a new block to the chain. 
In this implementation, the mineBlock() method simply adds a new block to the chain with a random transaction.

`Hashing Function`
A cryptographic `hashing function` is crucial for generating and validating block hashes. We will use the SHA-256 hashing algorithm.

```java
public String calculateHash() {
        // Hash calculation logic using the block's attributes and HashUtil
        // Example implementation:
        String data = index + timestamp.toString() + previousHash + transactions.toString() + nonce;
        return HashUtil.calculateSHA256(data);
    }
```
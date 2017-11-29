# Topic : Crypto currency: Data Structures and Algorithms

## Presenter: Mochan Shrestha

---

### Public/Private Keys and Digital Signatures

* Generate two keys (one private (*sk*) and one public (*pk*))
* Digital signatures: `signature = sign(sk, message)` can be quickly verified `verify(pk, message, sig)`
* But without the secret key, `sign(_sk_, message)` is computationally hard

---

### Bitcoin Address and Wallets

* Public Key: Bitcoin address (psuedonym, username)
  * Bitcoins are owned by a public key
* By signing a transaction with a secret key, you can transfer bitcoin to another address
  * Secret key controls the money. Don't lose it! Keep it safe!
* Bitcoin Wallet: Secret key manager, signer etc
* ECDSA - secp256k1 (https://github.com/bitcoin-core/secp256k1) - Original implementation from OpenSSL (https://github.com/bitcoin/bitcoin/commit/6e182686163ce3c15b878bd78c41d)

---

### Crytographic Hash Functions

* Takes any byte array as input and produces a fixed size output
* Properties of hash functions:
  * Given `x` and `H(x)`, it computationally difficult to find `y` such that `H(x) = H(y)`
  * Computationally difficult to change message and the hash to remain the same
  * Small changes in the messages results in a large change in the hash function
* Bitcoin uses SHA-256 hash function

---

### Blockchain

* Hash Pointer: Store the hash of the data along with the pointer to the data
* We will know if the data that the hash pointer points to has changed or not
* **Blockchain**: Replace pointers in a linked list with hash pointers
* When a new node is added, the previous node cannot be tampered without detection
* ![BlockChain](https://raw.githubusercontent.com/MochanShrestha/aadcpp-meetup-content/master/11-2017/cryptocurrency/blockchain.png)

---

### Merkle Tree

* Binary tree with hash pointers
* ![Merkle Tree](https://raw.githubusercontent.com/MochanShrestha/aadcpp-meetup-content/master/11-2017/cryptocurrency/MerkleTree.png)
* No data can be changed without changing the hash in the root
* Don't have to download the entire data set to check if a piece of data is valid
* Bitcoin transactions are hashed and `hashMerkleRoot` is the hash of the hashes

---

### Transactions

* Bitcoin transactions are the bitcoin's blocks in the blockchain
* Forms a ledger that can only be appended
* Multiple inputs and ouputs
* All the inputs are exhausted. Remaining must be transferred.
* Smallest denomination of a coin called a Satoshi and 10,000,000 Satoshis = 1 bitcoin

---

### Bitcoin Scripts

* Transactions inputs and outputs do not specify addresses, hashes or signatures but scripts
* Scripts contain all the data and have to be run successfully to claim a bitcoin
* Stack based language with cryptography supported instructions
* No loops and executes linearly. Runtime complexity is the length of the script
* Allows for smart contracts but most nodes whitelist scripts like pay to public key hash, pay to public key, pay to script hash
* Ethereum has extended this to a VM with a Turing complete script. Halting problem is avoided by just setting a cap on the execution time

---

### Distributed Consensus

* Bitcoin does not have a central authority to make blocks and record transactions
* It is on a P2P network (no central nodes, random topology with anonymous nodes)
  * Protocol takes a finite amount of time to agree on a same value
  * Agreed values must be produced by one of the nodes
* Byzantine General's Problem - many situations which have proven impossibility results
* When a new block is created, it is spread through the P2P using a gossip protocol. Each node tells every other node they know about new information.
* It executes a consensus protocol and the entire network decides on a new block to add to the blockchain
* Bitcoin has no consensus guarantee but very low probability that consensus was not reached

---

### Bitcoin Network

* In Bitcoin, when Alice wants to send Bob money, she broadcasts the transaction to every node she knows.
* Each node collects all the transactions they have heard about into a block
* If crypto signatures do not match, it is discarded. So, Alice cannot only try and send coins on addresses which she controls
* Alice's transaction is then put on a block by some node which gets to choose the next block in the blockchain
* All other nodes accept this block by putting the hash of the block on the next block in the blockchain

--- 

### Bitcoin Network Protocol

* Nodes will have to store the entire blockchain (140GB right now)
* Only relay transactions that the node has not seen before
* Only keep blocks that extend the longest chain
* Current information about the blockchain: http://blockchain.info

---

### Double Spend Attack

* Alice broadcasts transaction of bitcoin to Bob
* Alice again broadcasts another transaction to Adam (controlled by Alice) for the same coin
* Double spend attack if
  * Bob believes that Alice has sent him the bitcoins and does their part
  * Long term consensus that Alice sent Adam the bitcoin

---

### Block Reward

* The node that proposes the next node in the blockchain gets to add a reward transaction for doing so - currently 12.5 bitcoins
* The node chooses an address to send newly created bitcoins to (usually address controlled by the node)
* This is the only way bitcoins are created
* Very high incentive for the proposed block to reach consensus among peer nodes
* Dishonesty can cause block rejection and missed chance to collect the reward
  * Node thoroughly checks all transactions for errors
  * Propose a block that other nodes would likely accept
* Huge problem if one person controls large portion of the network

---

### Proof of Work

* Ideally we want to choose a random person in the network and let the person propose a new block and collect the reward
* We use a method to emulate the randomness by selecting nodes by a resource that no single person can monopolize
* Select nodes by their computing power
* Nodes compete for the right to create a block and the probability that they will create the node will be proportional to their computing power

---

### Hash Puzzle

* To create a block, find a `nonce` such that:
  * `H( prev_block_hash | nonce | {txs} ) < threshold`
* Only way to solve this puzzle is through brute force - keep trying nonces until the above condition is met
* Chance of creating a new block depends on your hashing power - how many hashes can you perform per second
* More computing power means more chance of reward
* `threshold` determines the difficulty which is adjustable to the global hashing power which is adjusted every two weeks
* https://blockchain.info/stats for current statistics

--- 

### Mining Puzzles

* Cheap to verify that puzzle has been solved
* Adjustable difficulty
* Progress free - chance of winning is proportional to the computation power - it is probabilistic and the one with the highest computing power does not always win

---

### Bitcoin Mining

* Bitcoin depends on miners doing the work.
  * Store the blockchain and send the blockchain to other nodes
  * Validate that transactions have no cryptographic errors
  * Do not let another miner dominate the network by using your own hash power
* Expected time until block reward is proportional to
  * `1 / fraction_of_global_hash_power`
  * Currently is in 100s of years if you become a bitcoin node

---

### Mining Pools

* Contribute hash power to a node and block rewards are distributed by the computation power contributed
* Mining shares - Approximated by sending near misses to the solution

---

### Transaction Fees

* Block reward is not the only way for miners to earn rewards
* By making output transaction smaller than the input transaction, miners can be rewarded for putting their transaction on the blockchain

---

### Bitcoin Constants (Hardcodes) and Implications

* 10 minutes block creation time
  * Difficulty adjusted with total hash global hash power
* 1MB in a block 
  * 250 bytes / transaction average
  * 7 transactions / second
* Mining rewards geometrically decay with number of blocks found
  * Started with 50 and goes to 50, 25, 12.5, 6.25, ...
  * Currently at 12.5 and thus total 21 million bitcoins

---

### Hard Forks

* If some node change their software and others don't such that the rules of validating blocks are different
  * the network splits into two
  * Network will never converge
* If you had bitcoins before the fork, you'll still have coins on the new fork
* A new block reward is not transferred across after a fork

---

### Alt-Coins

* Other bitcoin like networks starting with a new blockchain
* New algorithms, strategies, constants etc
* Bootstrap problem. Interdependent properties
  * Security of block-chain
  * Health of Mining Ecosystem
  * Value of Currency

---

### Proof of Stake or Deposit or Activity

* Instead of using computing power, alternate methods
  * Stake : amount of coins, age of coin
  * Deposit : deposit of coins to be considered

---

### Alternate Mining Puzzles

* SHA-256 is very ASIC friendly and so hash power has moved to ASIC manufacturing
* Memory hard mining puzzles that favor GPU over ASICs
  * Scrypt - Hashes of hashes
  * DAG - given random graph, find a directed acyclic graph is memory intensive

---

### Pseudo-Anonymity and Anonymity

* Bitcoin is not anonymous - you have a pseudonym that can be attached to a real life identity
* Mixing Services
  * Confuse the money trail in the blockchain
  * Bitcoins are put in together but different bitcoins are assigned out
* Zero-coin and zero-cash: Protocol level mixing

---

### Questions?

---

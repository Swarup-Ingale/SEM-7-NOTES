# Master Academic Study Guide: Mumbai University MLBC Module 04 Examination Answers

## Module 4: Cryptographic Foundations and Distributed Ledger Architecture

---

### Question 1 (10 Marks):
**(a) Define Blockchain Technology and explain its evolutionary history. Contrast Centralized, Decentralized, and Distributed systems across key architectural dimensions.**  
**(b) Detail the Six-Layer Architecture of Blockchain technology with a neat diagram. Explain the structure of a Block and the cryptographic mechanics of Block Linking.**

---

#### 1. Mumbai University Marking Scheme Rubric (10 Marks)

| Sub-Component | Evaluation Criteria | Allocated Marks |
| :--- | :--- | :--- |
| **Blockchain Definition & History** | Formal definition, genesis, transition from Stuart Haber/W. Scott Stornetta (1991) to Satoshi Nakamoto (2008 Bitcoin Whitepaper), and fundamental value proposition. | **2 Marks** |
| **System Architectural Comparison** | Comparative analysis matrix contrasting Centralized, Decentralized, and Distributed systems across governance, fault tolerance, transparency, and latency. | **2.5 Marks** |
| **Six-Layer Blockchain Architecture** | Neat ASCII architectural diagram depicting Data, Network, Consensus, Incentive/Execution, Contract, and Application layers with specific functionalities. | **3 Marks** |
| **Block Structure & Linking Mechanics** | Internal fields of Block Header and Block Body, hash pointer mechanics, Genesis block properties, and mathematical tamper-evidence propagation. | **2.5 Marks** |

---

#### 2. Part (a): Blockchain Definition, History, and System Architecture Comparison

##### Formal Definition of Blockchain
A **Blockchain** is a distributed, cryptographically secured, append-only immutable ledger maintained by a decentralized peer-to-peer (P2P) network of computational nodes without the intervention of a central coordinating intermediary. It groups verified transactional data into timestamped blocks cryptographically bound together into a sequential chain using cryptographic hash pointers.

##### Historical Evolution of Blockchain
The conceptual foundations of blockchain evolved through distinct cryptographic milestones:
1. **1991 (Cryptographic Timestamping)**: Stuart Haber and W. Scott Stornetta introduced cryptographically certified digital document timestamping using linked hash chains and Merkle trees to prevent backdating or altering digital records.
2. **1997–1998 (Proof of Work & Decentralized Currencies)**: Adam Back devised **Hashcash**, introducing Proof-of-Work to throttle denial-of-service and spam attacks. Concurrently, Wei Dai proposed **B-money** and Nick Szabo conceptualized **Bit Gold**, introducing decentralized electronic currency architectures reliant on cryptographic puzzle solutions.
3. **2008 (Bitcoin Genesis)**: Satoshi Nakamoto published the seminal whitepaper *"Bitcoin: A Peer-to-Peer Electronic Cash System"*, unifying peer-to-peer networking, asymmetric cryptography, Nakamoto consensus (Proof of Work), and economic game-theoretic incentives to resolve the notorious Double-Spending problem without a trusted third party.
4. **2013–2015 (Programmable Smart Contracts & Ethereum)**: Vitalik Buterin conceptualized Ethereum, expanding blockchain beyond monetary transfers into a Turing-complete decentralized computing platform powered by the Ethereum Virtual Machine (EVM) and self-executing Smart Contracts.
5. **2016–Present (Enterprise & Layer-2 Solutions)**: Evolution toward permissioned enterprise consortium frameworks (Hyperledger Fabric, R3 Corda) and Layer-2 scalability architectures (State Channels, Rollups, Sharding).

##### Architectural Comparison: Centralized vs. Decentralized vs. Distributed Systems

```
    [Centralized]               [Decentralized]              [Distributed]
        ( O )                       ( O )                       ( O )---( O )
       /  |  \                     /     \                      | \   / |
     (O) (O) (O)                 (O)     (O)                    |  (O)  |
     / \  |  / \                 / \     / \                    | /   \ |
    O   O O O   O               O   O   O   O                   ( O )---( O )
(Single Central Node)       (Multiple Regional Hubs)       (Autonomous Peer Nodes)
```

| Architectural Parameter | Centralized System | Decentralized System | Distributed System |
| :--- | :--- | :--- | :--- |
| **Authority & Governance** | Monolithic control under a single centralized administrator or organization. | Authority distributed among a network of equal peers governed by consensus protocols. | Computation and data spread across multiple processing units; may still have centralized logic. |
| **Single Point of Failure (SPOF)**| **Critical SPOF**: Failure of the central server crashes the entire system. | **No SPOF**: System maintains operational liveness despite concurrent node outages. | **Resilient**: Tasks fail over across nodes, but centralized master node failures can halt tasks. |
| **Data Replication & State** | Maintained within a central database; external clients hold only view access. | Every full node maintains an identical, verified copy of the entire ledger state. | Data is fragmented or partitioned (sharded) across computational clusters. |
| **Trust Model** | Subjective trust placed entirely in the centralized operator. | Trust-minimized; verified purely through mathematical cryptographic consensus. | Trust defined by network architecture, typically operating inside a private perimeter. |
| **Throughput & Scalability** | High transaction throughput ($>50,000$ TPS) with low confirmation latency. | Restricted throughput ($7-30$ TPS on Layer-1 PoW) due to global consensus overhead. | High parallel processing throughput via distributed computation pipelines. |
| **Auditability & Immutability** | Mutable: System administrators can modify, overwrite, or delete historical records. | Immutable: Cryptographic block linking prevents retrospective data alteration. | Dependent on storage engine; generally mutable unless configured with WORM storage. |

---

#### 3. Part (b): Six-Layer Blockchain Architecture and Block Linking Mechanics

##### The Six-Layer Blockchain Architecture
A robust blockchain network is architecturally decoupled into six distinct hierarchical functional layers:

```
┌────────────────────────────────────────────────────────────────────────┐
│ 6. APPLICATION LAYER                                                  │
│    User Interfaces, DApps, Wallets (MetaMask), Web3.js, Block Explorer │
├────────────────────────────────────────────────────────────────────────┤
│ 5. CONTRACT & EXECUTION LAYER                                          │
│    Smart Contracts, EVM Bytecode, Chaincode, Execution Logic, Gas Rules│
├────────────────────────────────────────────────────────────────────────┤
│ 4. INCENTIVE LAYER                                                     │
│    Tokenomics, Mining Block Rewards, Transaction Gas Fees, Slashing    │
├────────────────────────────────────────────────────────────────────────┤
│ 3. CONSENSUS LAYER                                                     │
│    Proof of Work (PoW), Proof of Stake (PoS), PBFT, Raft, Paxos        │
├────────────────────────────────────────────────────────────────────────┤
│ 2. NETWORK & PROPAGATION LAYER                                         │
│    P2P Topology, Gossip Protocol, Node Discovery, Block Validation/Relay│
├────────────────────────────────────────────────────────────────────────┤
│ 1. DATA LAYER                                                          │
│    Blocks, Hash Pointers, Merkle Trees, Asymmetric Keys, State Storage │
└────────────────────────────────────────────────────────────────────────┘
```

1. **Data Layer**: Serves as the foundational physical and logical data representation. Encapsulates transactional records, digital signatures (ECDSA), cryptographic hash pointers (SHA-256), binary Merkle Trees, and raw state key-value databases (LevelDB / RocksDB).
2. **Network / Propagation Layer**: Manages the decentralized peer-to-peer (P2P) networking topology. Utilizes discovery protocols (Kademlia DHT) and Gossip dissemination protocols to broadcast transactions and freshly mined blocks asynchronously to all participating network nodes.
3. **Consensus Layer**: The algorithmic core enforcing Byzantine Fault Tolerance (BFT) and absolute state agreement across mutual-distrusting participants without central coordination. Implements consensus mechanisms like Proof of Work (PoW), Proof of Stake (PoS), and Practical Byzantine Fault Tolerance (PBFT).
4. **Incentive Layer**: Formulates economic game-theoretic models (Tokenomics). Directs currency emission models, allocates block proposal subsidies (coinbase transactions), computes dynamic transaction processing fees (Gas), and imposes slashing penalties to mathematically guarantee honest participant behavior.
5. **Contract & Execution Layer**: Houses the programmable computational infrastructure. Encompasses smart contract source code (Solidity, Vyper), virtual runtime engines (Ethereum Virtual Machine - EVM, eWASM), execution sandboxes, and state-transition logic.
6. **Application Layer**: Direct user-facing interfaces. Comprises Decentralized Applications (DApps), decentralized finance (DeFi) platforms, cryptographic key-management wallets, and client integration libraries (Web3.js, Ethers.js, RPC interfaces).

---

##### Block Structure & Cryptographic Linking Mechanics

A blockchain ledger organizes data into chronologically arranged blocks consisting of a **Block Header** and a **Block Body**.

```
========================= BLOCK N-1 =========================
[Block Header]
├── Version: 0x20000000
├── Prev Block Hash: 00000000000000000007ab... (Points to Block N-2)
├── Merkle Root: 4a5e1e4baab89f3a32518a88c31bc87f618f76673e2cc77ab2127b7afdeda33b
├── Timestamp: 1714567890 (Unix Epoch)
├── Difficulty Target (Bits): 0x170586bf
└── Nonce: 2083236893
[Block Body]
└── [Tx 0 (Coinbase), Tx 1, Tx 2, ..., Tx M]
                       ▲
                       │ Cryptographic Link: PrevBlockHash = SHA-256(SHA-256(Header N-1))
========================= BLOCK N ===========================
[Block Header]
├── Version: 0x20000000
├── Prev Block Hash: 00000000000000000004bc... (Double-SHA-256 of Block N-1 Header)
├── Merkle Root: 8c14f0db3df150123e6f3db530476bc60fa79b9ac852e50279b3ec05316e9234
├── Timestamp: 1714568490
├── Difficulty Target (Bits): 0x170586bf
└── Nonce: 1845239102
[Block Body]
└── [Tx 0 (Coinbase), Tx 1, Tx 2, ..., Tx K]
```

###### Block Header Fields Breakdown (Standard 80-Byte Bitcoin Header)
1. **Block Version (4 Bytes)**: Tracks protocol consensus rules, software upgrades, and BIP soft-fork readiness.
2. **Previous Block Hash (32 Bytes)**: A double-SHA-256 cryptographic hash digest of the parent block header:
   $$\text{PrevBlockHash}_N = \text{SHA256}(\text{SHA256}(\text{Header}_{N-1}))$$
   This field binds Block $N$ inextricably to Block $N-1$.
3. **Merkle Root Hash (32 Bytes)**: A cryptographic 256-bit hash representing the hierarchical binary Merkle tree root of all transactions contained in the Block Body.
4. **Timestamp (4 Bytes)**: Unix epoch time indicating when block mining commenced.
5. **Difficulty Target / Bits (4 Bytes)**: Compact cryptographic encoding of the current PoW mining difficulty threshold $T$.
6. **Nonce (4 Bytes)**: An arbitrary 32-bit counter incremented by miners to satisfy the Proof-of-Work inequality:
   $$\text{SHA256}(\text{SHA256}(\text{Header}(\text{Nonce}))) < \text{Target}$$

###### Mathematical Tamper Resistance and Cascade Invalidation
Consider an adversary attempting to alter a historical transaction $Tx_k$ inside Block $N-j$:
1. Modifying a single character or byte in $Tx_k$ alters its cryptographic hash digest $H(Tx_k)$ due to the **Avalanche Effect**.
2. Because transaction hashes are concatenated pairwise up the Merkle tree, the root hash $\text{MerkleRoot}_{N-j}$ changes completely:
   $$\text{MerkleRoot}_{N-j}' \neq \text{MerkleRoot}_{N-j}$$
3. Altering $\text{MerkleRoot}_{N-j}$ modifies the 80-byte header of Block $N-j$, which completely changes its header hash digest:
   $$\text{Hash}_{N-j}' = \text{SHA256}(\text{SHA256}(\text{Header}_{N-j}')) \neq \text{Hash}_{N-j}$$
4. Consequently, Block $(N-j+1)$, which contains $\text{PrevBlockHash} = \text{Hash}_{N-j}$, detects a cryptographic pointer mismatch. Its stored link points to an invalid or broken reference.
5. To restore ledger integrity, the attacker must recompute the cryptographic Proof-of-Work (nonce search) for Block $N-j$, and sequentially recompute every subsequent block up to the tip of the chain $(N-j+1, \dots, N)$ faster than the cumulative computational hash power of all honest nodes combined ($>51\%$ computational hash power required), rendering the system practically immutable.

---

### Question 2 (10 Marks):
**(a) Explain Cryptographic Hash Functions. Detail the internal architecture and compression function of SHA-256 along with its five core mathematical properties.**  
**(b) Detail the mathematical foundations of Elliptic Curve Cryptography (ECC) over the secp256k1 curve. Explain the generation of ECDSA Digital Signatures and the mathematical verification process.**

---

#### 1. Mumbai University Marking Scheme Rubric (10 Marks)

| Sub-Component | Evaluation Criteria | Allocated Marks |
| :--- | :--- | :--- |
| **Cryptographic Hash Properties** | Clear definitions of Pre-image, Second pre-image, Collision resistance, Avalanche effect, and Puzzle-friendliness. | **2 Marks** |
| **SHA-256 Architecture & Pipeline**| Merkle-Damgård construction, 512-bit message block padding, 64-round compression loop, message schedule ($W_t$), and state registers ($A-H$). | **3 Marks** |
| **ECC secp256k1 Mathematics** | Weierstrass elliptic curve equation over finite field $\mathbb{F}_p$, point addition formulas, scalar multiplication $Q = d \times G$, and Discrete Logarithm hardness. | **2.5 Marks** |
| **ECDSA Signature & Verification** | Key generation, ephemeral nonce $k$, computing signature pair $(r, s)$, and public key verification formula $R' = (u_1 G + u_2 Q)$. | **2.5 Marks** |

---

#### 2. Part (a): SHA-256 Hash Architecture and Mathematical Properties

##### Core Cryptographic Properties of Hash Functions
A cryptographic hash function $H: \{0, 1\}^* \to \{0, 1\}^n$ maps arbitrary-length binary inputs to a deterministic fixed-length $n$-bit digest (for SHA-256, $n = 256$). To ensure blockchain security, it must satisfy five mathematical properties:

1. **Pre-image Resistance (One-Way Property)**: Given an arbitrary output hash $y$, it is computationally infeasible to determine the original input message $x$ such that $H(x) = y$. Inversion requires brute-force search with time complexity $O(2^n)$ (for SHA-256: $2^{256}$ operations).
2. **Second Pre-image Resistance (Weak Collision Resistance)**: Given a specific input $x_1$, it is computationally infeasible to find an alternate input $x_2 \neq x_1$ such that $H(x_1) = H(x_2)$.
3. **Collision Resistance (Strong Collision Resistance)**: It is computationally infeasible to locate *any* two distinct inputs $x_1 \neq x_2$ such that $H(x_1) = H(x_2)$. Under the **Birthday Paradox**, finding collisions requires $O(2^{n/2})$ operations ($2^{128}$ evaluations for SHA-256).
4. **Avalanche Effect (High Sensitivity)**: A minute modification in the input (e.g., flipping a single bit) must cause a catastrophic, uncorrelated change in the output digest, flipping approximately $50\%$ of the output bits.
5. **Puzzle Friendliness**: Given a target value $Y$ and an arbitrary $k$-bit prefix, it is computationally impossible to select an input $X$ that yields $H(K \parallel X) = Y$ better than by evaluating random guesses, forming the mathematical cornerstone of Proof-of-Work mining.

---

##### SHA-256 Internal Compression Architecture
SHA-256 follows the **Merkle-Damgård construction** using the Davies-Meyer compression function.

```
[Input Message M] (Arbitrary length L bits)
        │
        ▼
[Padding Phase]: Append '1' bit, k '0' bits, and 64-bit Big-Endian Length L
        │  (Resulting Length = Multiple of 512 bits: N * 512)
        ▼
   ┌───────────────┐     ┌───────────────┐           ┌───────────────┐
   │ Block M^(1)   │     │ Block M^(2)   │           │ Block M^(N)   │
   └───────┬───────┘     └───────┬───────┘           └───────┬───────┘
           │                     │                           │
  IV ────►( f )─────────►( H^(1) )──►( f )───► ... ────►( H^(N-1) )──►( f )────► Final 256-bit Digest
```

###### Phase 1: Preprocessing and Message Padding
1. A single `'1'` bit is appended to the message: $M \parallel 1$.
2. $k$ zero bits `'0'` are appended, where $k$ is the smallest non-negative integer satisfying:
   $$L + 1 + k \equiv 448 \pmod{512}$$
3. The original message length $L$ (expressed as a 64-bit big-endian integer) is appended, producing a padded message whose total bit length is an exact multiple of 512 bits ($N \times 512$).
4. The padded message is divided into $N$ successive 512-bit message blocks: $M^{(1)}, M^{(2)}, \dots, M^{(N)}$.

###### Phase 2: Message Schedule Expansion
Each 512-bit block $M^{(i)}$ is split into sixteen 32-bit words $W_0, W_1, \dots, W_{15}$. These are expanded into an array of sixty-four 32-bit words $W_0, \dots, W_{63}$ using rotation and shift primitives:

$$W_t = \sigma_1(W_{t-2}) + W_{t-7} + \sigma_0(W_{t-15}) + W_{t-16} \quad (16 \le t \le 63)$$

where:
$$\sigma_0(x) = \text{ROTR}^7(x) \oplus \text{ROTR}^{18}(x) \oplus \text{SHR}^3(x)$$
$$\sigma_1(x) = \text{ROTR}^{17}(x) \oplus \text{ROTR}^{19}(x) \oplus \text{SHR}^{10}(x)$$

###### Phase 3: The 64-Round Compression Loop
The internal working state consists of eight 32-bit registers initialized to specific fractional-part constants of prime square roots: $a, b, c, d, e, f, g, h$. For each round $t \in [0, 63]$:

$$T_1 = h + \Sigma_1(e) + \text{Ch}(e, f, g) + K_t + W_t$$
$$T_2 = \Sigma_0(a) + \text{Maj}(a, b, c)$$
$$h = g; \quad g = f; \quad f = e; \quad e = d + T_1; \quad d = c; \quad c = b; \quad b = a; \quad a = T_1 + T_2$$

where bitwise non-linear functions are defined as:
$$\text{Ch}(e, f, g) = (e \wedge f) \oplus (\neg e \wedge g) \quad \text{(Choice Function)}$$
$$\text{Maj}(a, b, c) = (a \wedge b) \oplus (a \wedge c) \oplus (b \wedge c) \quad \text{(Majority Function)}$$
$$\Sigma_0(a) = \text{ROTR}^2(a) \oplus \text{ROTR}^{13}(a) \oplus \text{ROTR}^{22}(a)$$
$$\Sigma_1(e) = \text{ROTR}^6(e) \oplus \text{ROTR}^{11}(e) \oplus \text{ROTR}^{25}(e)$$
$K_t$ represents 64 pre-defined 32-bit round constants derived from the cube roots of the first 64 primes. The resulting register outputs are added modulo $2^{32}$ to the previous intermediate state.

---

#### 3. Part (b): Elliptic Curve Cryptography (secp256k1) and ECDSA Digital Signatures

##### Mathematical Foundations of ECC over Finite Fields
Elliptic Curve Cryptography establishes asymmetric key pairs leveraging the algebraic group properties of non-singular elliptic curves over finite Galois Fields $\mathbb{F}_p$. Production blockchains (Bitcoin and Ethereum) standardize on the **secp256k1** curve, specified as a Koblitz curve in Short Weierstrass form:

$$y^2 \equiv x^3 + 7 \pmod p$$

defined over prime field $\mathbb{F}_p$, where $p$ is the 256-bit prime:
$$p = 2^{256} - 2^{32} - 977 = \text{FFFFFFFF FFFFFFFF FFFFFFFF FFFFFFFF FFFFFFFF FFFFFFFF FFFFFFFE FFFFFC2F}$$

###### Geometric Point Addition and Point Doubling Formulas
Given two points $P(x_1, y_1)$ and $Q(x_2, y_2)$ on the curve:
1. **Point Addition ($P \neq Q$)**: The line intersecting $P$ and $Q$ intersects the curve at a third point; reflecting across the $x$-axis yields $R = P + Q = (x_3, y_3)$:
   $$\lambda = \frac{y_2 - y_1}{x_2 - x_1} \pmod p$$
   $$x_3 = \lambda^2 - x_1 - x_2 \pmod p, \quad y_3 = \lambda(x_1 - x_3) - y_1 \pmod p$$
2. **Point Doubling ($P = Q$)**: Evaluating the tangent line slope at point $P$:
   $$\lambda = \frac{3x_1^2}{2y_1} \pmod p$$
   $$x_3 = \lambda^2 - 2x_1 \pmod p, \quad y_3 = \lambda(x_1 - x_3) - y_1 \pmod p$$

##### Key Generation Mechanics
1. **Private Key ($d$)**: A cryptographically secure random 256-bit scalar integer chosen from range $[1, n-1]$:
   $$d \in [1, n-1]$$
   where $n$ is the fixed prime order of base generator point $G$.
2. **Public Key ($Q$)**: Derived via **Scalar Point Multiplication** (computed in $O(\log_2 d)$ steps via Double-and-Add):
   $$Q = d \times G$$
   The **Elliptic Curve Discrete Logarithm Problem (ECDLP)** ensures that while computing $Q$ from $d$ is efficient, calculating scalar private key $d$ given public point $Q$ and generator $G$ is computationally intractable, requiring $O(\sqrt{n}) \approx 2^{128}$ Pollard's rho operations.

---

##### ECDSA Signature Generation and Verification Pipeline

```
========================= SIGNING PIPELINE =========================
[Message M] ──► SHA-256 ──► [Hash e = H(M)]
                                 │
[Random Nonce k] ──► k * G ──► Point (x_1, y_1) ──► r = x_1 mod n
                                                          │
[Private Key d] ──────────────────────────────────────────┼──► s = k⁻¹(e + d*r) mod n
                                                          ▼
                                            Signature Pair: (r, s)

======================= VERIFICATION PIPELINE =======================
[Signature (r, s)], [Message M], [Public Key Q]
        │
        ├──► Compute: w = s⁻¹ mod n
        ├──► Compute: u₁ = e * w mod n   (where e = H(M))
        └──► Compute: u₂ = r * w mod n
                    │
                    ▼
        Calculate Curve Point: R' = (u₁ * G) + (u₂ * Q) = (x₁', y₁')
                    │
                    ▼
        VALID IF: r ≡ x₁' mod n  (Otherwise REJECT)
```

###### Signature Generation Algorithm
Given message $m$, private key $d$, and curve parameters $(p, n, G)$:
1. Calculate the cryptographic hash digest: $e = \text{SHA256}(m)$.
2. Select a cryptographically secure, random ephemeral nonce $k \in [1, n-1]$. *(Reusing or leaking $k$ enables instantaneous private key derivation).*
3. Compute curve point: $(x_1, y_1) = k \times G$.
4. Calculate signature scalar $r$:
   $$r = x_1 \pmod n \quad (\text{if } r = 0, \text{ choose a new } k)$$
5. Calculate signature scalar $s$:
   $$s = k^{-1} (e + d \cdot r) \pmod n \quad (\text{if } s = 0, \text{ choose a new } k)$$
6. Output digital signature pair: $(r, s)$.

###### Signature Verification Proof
A verifier holding message $m$, signature $(r, s)$, and public key $Q$:
1. Verify that $r, s \in [1, n-1]$.
2. Compute $e = \text{SHA256}(m)$ and modular inverse $w = s^{-1} \pmod n$.
3. Compute intermediate scalars:
   $$u_1 = e \cdot w \pmod n, \quad u_2 = r \cdot w \pmod n$$
4. Compute curve point: $R' = u_1 \times G + u_2 \times Q = (x_1', y_1')$.
5. The signature is cryptographically **VALID** if and only if:
   $$r \equiv x_1' \pmod n$$

###### Mathematical Proof of Correctness
Substituting $Q = d \times G$ and $w = s^{-1}$:
$$R' = u_1 G + u_2 Q = (e \cdot w) G + (r \cdot w) (d \cdot G) = w (e + d \cdot r) G$$
Since $s = k^{-1}(e + d \cdot r) \pmod n$, we have $s \cdot k = (e + d \cdot r) \pmod n$. Thus:
$$k = s^{-1}(e + d \cdot r) = w(e + d \cdot r) \pmod n$$
Substituting $k$ back into the point equation yields:
$$R' = k \times G = (x_1, y_1)$$
Hence, $x_1' = x_1$, proving $r \equiv x_1' \pmod n$.

---

### Question 3 (10 Marks):
**(a) What is a Merkle Tree? Explain its construction, hashing mechanics, and role in ensuring data integrity within a block.**  
**(b) Detail the concept of Simplified Payment Verification (SPV) light clients. Derive the mathematical verification complexity of Merkle Audit Paths and contrast it with full ledger verification.**

---

#### 1. Mumbai University Marking Scheme Rubric (10 Marks)

| Sub-Component | Evaluation Criteria | Allocated Marks |
| :--- | :--- | :--- |
| **Merkle Tree Architecture** | Definition, binary tree structure, pairwise concatenation, double-SHA-256 operations, and handling odd transaction counts. | **3 Marks** |
| **Data Integrity & Tamper Evidence**| Demonstration of how leaf modification cascades to the Merkle Root, and role of Merkle Root in Block Header binding. | **2 Marks** |
| **SPV Light Client Concept** | Definition of SPV, architecture of Light Nodes vs Full Nodes, and bandwidth/storage optimizations. | **2 Marks** |
| **Audit Path Derivation & Complexity**| Step-by-step audit path example, mathematical verification proof, and rigorous $O(\log_2 N)$ vs $O(N)$ complexity derivation with numerical comparison. | **3 Marks** |

---

#### 2. Part (a): Merkle Tree Construction and Hashing Mechanics

##### Architectural Overview of Merkle Trees
A **Merkle Tree** (Binary Hash Tree) is a hierarchical cryptographic data structure wherein every leaf node is labeled with the cryptographic hash of a raw data block (transaction), and every non-leaf (parent) node is labeled with the cryptographic hash of the concatenated labels of its child nodes. Introduced by Ralph Merkle in 1979, it enables secure, highly efficient verification of large datasets.

```
                     [ Merkle Root Hash: H_ABCD ]
                                   │
                   ┌───────────────┴───────────────┐
                   │                               │
         [ Hash Node: H_AB ]             [ Hash Node: H_CD ]
                   │                               │
           ┌───────┴───────┐               ┌───────┴───────┐
           │               │               │               │
      [ H(Tx_A) ]     [ H(Tx_B) ]     [ H(Tx_C) ]     [ H(Tx_D) ]
           ▲               ▲               ▲               ▲
           │               │               │               │
       [ Tx A ]        [ Tx B ]        [ Tx C ]        [ Tx D ]
```

##### Mathematical Construction and Hashing Mechanics
Consider a block body containing four transactions: $Tx_A, Tx_B, Tx_C, Tx_D$:

1. **Leaf Level Computation**: Each raw transaction is serialized and hashed using double-SHA-256 ($\text{SHA256d}$):
   $$H_A = \text{SHA256}(\text{SHA256}(Tx_A))$$
   $$H_B = \text{SHA256}(\text{SHA256}(Tx_B))$$
   $$H_C = \text{SHA256}(\text{SHA256}(Tx_C))$$
   $$H_D = \text{SHA256}(\text{SHA256}(Tx_D))$$
2. **Intermediate Parent Node Computation**: Sibling leaf hashes are concatenated in binary byte order and hashed:
   $$H_{AB} = \text{SHA256}(\text{SHA256}(H_A \parallel H_B))$$
   $$H_{CD} = \text{SHA256}(\text{SHA256}(H_C \parallel H_D))$$
3. **Top Merkle Root Computation**: Sibling parent hashes are concatenated and hashed to yield the unique 32-byte Merkle Root:
   $$\text{Merkle Root} = H_{ABCD} = \text{SHA256}(\text{SHA256}(H_{AB} \parallel H_{CD}))$$
4. **Handling Odd Transaction Counts**: If an odd number of transactions exists at any tree level, the final unpaired hash is duplicated and concatenated with itself:
   $$H_{odd} = \text{SHA256}(\text{SHA256}(H_N \parallel H_N))$$

##### Role of the Merkle Root in Block Integrity
The Merkle Root is stored directly inside the fixed 80-byte **Block Header**. This provides significant architectural advantages:
* **Separation of Header and Payload**: Full blocks can be several megabytes, but the header remains constant at 80 bytes.
* **Tamper Evidence**: Modifying any transaction $Tx_k$ alters its leaf hash $H_k$, which cascades upward to alter every parent hash up to the Merkle Root. If the root changes, the block header hash changes, breaking the cryptographic chain link to the next block.

---

#### 3. Part (b): Simplified Payment Verification (SPV) and Audit Path Complexity

##### Concept of SPV Light Clients
In public blockchains like Bitcoin, running a **Full Node** requires downloading, validating, and persistently storing the entire ledger history ($>550\text{ GB}$), demanding significant disk storage and I/O bandwidth.

To enable secure blockchain access on mobile devices and resource-constrained environments, Satoshi Nakamoto designed **Simplified Payment Verification (SPV)**:
* **SPV Light Nodes** do not download transactions or execute state scripts.
* They download **only the 80-byte block headers** of the longest Proof-of-Work chain (consuming approximately $4.2\text{ MB}$ per year).
* When an SPV node needs to verify whether a specific transaction $Tx_K$ is confirmed in Block $N$, it requests a cryptographic **Merkle Audit Path (Authentication Path)** from a connected full node.

---

##### Merkle Audit Path Verification Walkthrough
Suppose an SPV client wishes to verify that transaction $Tx_C$ is included in a block with Merkle Root $H_{ABCD}$.

```
                 [ Target Root: H_ABCD ] (Stored in Local Header)
                               ▲
                      =========│=========
                      │Recomputed H_ABCD│
                      =========▲=========
                               │
               ┌───────────────┴───────────────┐
               │                               │
        [ PROOF: H_AB ]               [ Recompute H_CD ]
        (Provided by Full Node)                ▲
                                               │
                               ┌───────────────┴───────────────┐
                               │                               │
                        [ Recompute H_C ]               [ PROOF: H_D ]
                               ▲                        (Provided by Full Node)
                               │
                          [ Target Tx_C ]
```

1. The SPV client hashes the target transaction to obtain $H_C = \text{SHA256d}(Tx_C)$.
2. The full node provides the minimal cryptographic **Merkle Audit Path** for $Tx_C$, which contains only two hashes:
   $$\text{Audit Path} = \{ H_D, H_{AB} \}$$
3. The SPV client computes the intermediate parent hash:
   $$H_{CD}' = \text{SHA256d}(H_C \parallel H_D)$$
4. The SPV client computes the candidate Merkle root:
   $$H_{ABCD}' = \text{SHA256d}(H_{AB} \parallel H_{CD}')$$
5. The SPV client compares $H_{ABCD}'$ against the authoritative **Merkle Root** stored in the locally validated block header:
   $$\text{If } H_{ABCD}' == H_{ABCD} \implies \text{Transaction is Valid and Confirmed in Block}$$
   Because hash collisions are computationally infeasible under SHA-256, it is mathematically impossible for an attacker to generate a fake transaction that matches the Merkle root without finding a collision.

---

##### Mathematical Complexity Derivation: Full Ledger vs. SPV Proof

###### Verification Time Complexity
* **Full Node Approach**: Must verify all $N$ transactions in the block:
  $$\text{Complexity}_{\text{Full}} = O(N)$$
* **SPV Light Client Approach**: A balanced binary tree of $N$ leaves has tree depth $h$:
  $$h = \lceil \log_2 N \rceil$$
  Verifying the Merkle path requires exactly $\lceil \log_2 N \rceil$ pairwise concatenations and hash computations:
  $$\text{Complexity}_{\text{SPV}} = O(\log_2 N)$$

###### Bandwidth & Storage Comparison Table

| Metric / Parameter | Full Ledger Verification | SPV Merkle Path Verification | Efficiency Gain Factor |
| :--- | :--- | :--- | :--- |
| **Data Transmission per Block** | Full Block Payload: $\sim 2\text{ MB} - 4\text{ MB}$ | Header ($80\text{ B}$) + Path ($\log_2 N \times 32\text{ B}$) | $>99.5\%$ reduction |
| **Computational Complexity** | Linear: $O(N)$ hash validations | Logarithmic: $O(\log_2 N)$ hash validations | Exponential speedup |
| **Storage Requirement ($10^6$ Blocks)**| $>550\text{ GB}$ (Complete ledger) | $\sim 80\text{ MB}$ (Headers only) | $\sim 7,000\times$ storage saving |

###### Numerical Proof with $N = 4,096$ Transactions:
* Full verification requires downloading and processing $N = 4,096$ transactions ($\approx 1.5\text{ MB}$).
* SPV verification requires an audit path containing only:
  $$\text{Path Length} = \log_2(4096) = 12 \text{ hashes}$$
  $$\text{Proof Size} = 12 \times 32 \text{ bytes} = 384 \text{ bytes}$$
This represents an exponential reduction from linear $O(N)$ to logarithmic $O(\log_2 N)$ complexity.

---

### Question 4 (10 Marks):
**(a) Explain the fundamental concepts of Game Theory applied to Blockchain. Detail the Nash Equilibrium and analyze the Prisoner's Dilemma with its payoff matrix.**  
**(b) Detail the Byzantine Generals Problem in distributed computing. Explain the Lamport-Shostak-Pease condition ($N \ge 3f + 1$) and contrast Zero-Sum vs. Non-Zero-Sum games in mining incentives.**

---

#### 1. Mumbai University Marking Scheme Rubric (10 Marks)

| Sub-Component | Evaluation Criteria | Allocated Marks |
| :--- | :--- | :--- |
| **Game Theory & Nash Equilibrium**| Strategic game formulation (Players, Strategies, Payoffs), formal definition of Nash Equilibrium, and strategic stability. | **2.5 Marks** |
| **Prisoner's Dilemma Payoff Matrix**| Payoff matrix formulation, dominant strategy analysis (Defect-Defect), Pareto efficiency vs. Nash equilibrium, and blockchain context. | **2.5 Marks** |
| **Byzantine Generals Problem** | Historical problem statement, traitor scenarios, oral message exchange steps, and rigorous derivation of $N \ge 3f + 1$. | **3 Marks** |
| **Zero-Sum vs. Non-Zero-Sum Mining**| Mathematical distinction, hash race zero-sum dynamics, and positive-sum network growth and incentive alignment. | **2 Marks** |

---

#### 2. Part (a): Game Theory Foundations, Nash Equilibrium, and the Prisoner's Dilemma

##### Strategic Game Foundations in Blockchain
A distributed decentralized blockchain system relies on economic game theory to ensure that independent, rational, and potentially adversarial participants coordinate to maintain a single source of truth.

A game in standard normal form is defined by the triple:
$$\Gamma = \langle \mathcal{N}, (\mathcal{S}_i)_{i \in \mathcal{N}}, (u_i)_{i \in \mathcal{N}} \rangle$$
where:
* $\mathcal{N} = \{1, 2, \dots, n\}$ is the set of participating players (e.g., miners, validators).
* $\mathcal{S}_i$ denotes the set of available strategies for player $i$. A strategy profile is $\mathbf{s} = (s_1, s_2, \dots, s_n) \in \mathcal{S}$.
* $u_i: \mathcal{S} \to \mathbb{R}$ represents the utility/payoff function mapping strategies to expected returns (e.g., block rewards minus hardware/electricity expenses).

---

##### Formal Definition of Nash Equilibrium
A strategy profile $\mathbf{s}^* = (s_1^*, s_2^*, \dots, s_n^*) \in \mathcal{S}$ constitutes a **Nash Equilibrium** if no player $i$ can unilaterally deviate from their chosen strategy $s_i^*$ to an alternative strategy $s_i \in \mathcal{S}_i$ to increase their expected payoff, holding all other players' strategies fixed:

$$u_i(s_i^*, \mathbf{s}_{-i}^*) \ge u_i(s_i, \mathbf{s}_{-i}^*) \quad \forall s_i \in \mathcal{S}_i, \quad \forall i \in \mathcal{N}$$

where $\mathbf{s}_{-i}^*$ denotes the strategy choices of all participants excluding player $i$.

###### Relevance to Blockchain Protocol Design
Nakamoto Consensus aligns player incentives so that following the honest consensus rules (extending the longest chain, validating valid transactions) forms a **Nash Equilibrium**. If a miner unilaterally attempts to broadcast invalid transactions or mine on an orphaned block, honest nodes reject the block. The rogue miner forfeits the block subsidy and transaction fees while bearing $100\%$ of the computational energy cost, making malicious deviations economically irrational.

---

##### The Prisoner's Dilemma: Payoff Matrix and Strategic Tension
The **Prisoner's Dilemma** illustrates why rational individual strategies can result in suboptimal collective outcomes.

Two suspects ($A$ and $B$) are arrested and interrogated separately. Each suspect has two pure strategies: **Cooperate** (remain silent) or **Defect** (betray the partner).

###### Strategic Payoff Matrix (Years in Prison: Represented as Negative Utilities)

| Player A \ Player B | Cooperate (Silent) | Defect (Betray) |
| :--- | :--- | :--- |
| **Cooperate (Silent)** | $(-1, -1)$ [Pareto Optimal] | $(-10, 0)$ [Exploitation] |
| **Defect (Betray)** | $(0, -10)$ [Free-Rider Gain] | **$(-5, -5)$ [Nash Equilibrium]** |

###### Strategic Equilibrium Analysis
1. **Player A's Rational Choice**:
   * If Player B Cooperates: Defecting gives $0$ years vs. Cooperating's $-1$ year $\implies$ **Defect is superior**.
   * If Player B Defects: Defecting gives $-5$ years vs. Cooperating's $-10$ years $\implies$ **Defect is superior**.
   * Therefore, **Defect** is a strictly dominant strategy for Player A.
2. **Player B's Rational Choice**: By symmetry, **Defect** is also a strictly dominant strategy for Player B.
3. **Outcome**: The unique Nash Equilibrium is **$(\text{Defect}, \text{Defect})$** yielding payoff $(-5, -5)$. However, the cooperative strategy profile $(\text{Cooperate}, \text{Cooperate})$ yields $(-1, -1)$, which is **Pareto Optimal** but unstable without an enforcement mechanism.

###### Application to Blockchain Security
In distributed peer-to-peer networks, "Defecting" corresponds to broadcasting invalid blocks, double-spending, or withholding data. Blockchain overcomes the Prisoner's Dilemma trap by introducing:
* **Repeated Games (Infinite Horizon)**: Nodes participate indefinitely; uncooperative behavior triggers punishment across subsequent rounds.
* **Economic Collateral & Rewards**: Protocol rewards honest validation ($+\text{Reward}$) and imposes severe financial penalties ($\text{Slashed Collateral} + \text{Burned Electricity}$), shifting the dominant strategy from Defect to Cooperate.

---

#### 3. Part (b): Byzantine Generals Problem, Threshold Bounds, and Mining Game Theory

##### The Byzantine Generals Problem (Lamport, Shostak, Pease - 1982)
The **Byzantine Generals Problem** is a foundational thought experiment modeling consensus across distributed, un-trusted communication networks:

A group of Byzantine army divisions surrounds an enemy city. Each division is commanded by a general. The generals must reach collective consensus on a unified battle plan: **Attack** or **Retreat**. Communication occurs exclusively via pairwise messengers. However, one or more generals (or messengers) may be traitors attempting to prevent honest generals from reaching an agreement.

```
                  [ General 1 (Commander) ]
                             │
            ┌────────────────┴────────────────┐
            ▼ (Attack)                        ▼ (Attack)
   [ General 2 (Honest) ] ──────────────► [ General 3 (Traitor) ]
                              (Retreat)
```

###### Consensus Requirements:
1. **Agreement**: All honest generals decide on the identical battle plan.
2. **Validity**: If the commanding general is honest, every honest general obeys the commander's issued order.

---

##### Mathematical Derivation of the $N \ge 3f + 1$ Bound
In a purely oral messaging network (where messages cannot be cryptographically signed with unforgeable signatures), consensus is impossible if the total number of faulty/traitorous nodes $f$ equals or exceeds one-third ($33.3\%$) of the total network nodes $N$.

###### Theorem:
To achieve Byzantine Fault Tolerance in an oral message passing system with $f$ faulty nodes, the network must contain at least:
$$N \ge 3f + 1$$

###### Proof by Contradiction for the Base Case ($N = 3, f = 1$):
Assume a 3-node network ($N=3$) can tolerate $f=1$ traitor.

* **Scenario 1 (Traitorous Lieutenant)**:
  * Commander $C$ is honest and orders **Attack**.
  * Lieutenant $L_1$ is honest; Lieutenant $L_2$ is a traitor.
  * $C$ sends **Attack** to both $L_1$ and $L_2$.
  * To sow discord, $L_2$ tells $L_1$: *"The commander told me to Retreat"*.
  * $L_1$ receives contradictory inputs: **Attack** from $C$, and **Retreat** from $L_2$.
* **Scenario 2 (Traitorous Commander)**:
  * Commander $C$ is a traitor; Lieutenants $L_1$ and $L_2$ are honest.
  * $C$ sends **Attack** to $L_1$, but sends **Retreat** to $L_2$.
  * $L_1$ and $L_2$ communicate: $L_2$ tells $L_1$: *"The commander told me to Retreat"*.
  * From $L_1$'s perspective, **Scenario 1 and Scenario 2 are indistinguishable**: $L_1$ receives **Attack** from $C$ and **Retreat** from $L_2$ in both cases.
  * If $L_1$ obeys $C$ (Attack), then in Scenario 2 $L_1$ attacks while $L_2$ retreats, violating Agreement.
  * If $L_1$ assumes $C$ is a traitor and retreats, then in Scenario 1 $L_1$ disobeys an honest commander, violating Validity.

Thus, $N=3$ cannot tolerate $f=1$ traitor. By general induction, reaching consensus requires:
$$N \ge 3f + 1 \implies f < \frac{N}{3}$$
Honest nodes must constitute strictly more than two-thirds ($>66.6\%$) of the network.

*(Note: When unforgeable digital signatures are introduced via ECDSA, signed messages enable Practical Byzantine Fault Tolerance to handle arbitrary Byzantine faults up to $f < N/2$ in synchronous assumptions).*

---

##### Zero-Sum vs. Non-Zero-Sum Games in Blockchain Mining

```
      [ ZERO-SUM MINING RACE ]               [ NON-ZERO-SUM NETWORK ECOSYSTEM ]
    Total Reward R per Block = Fixed          Utility = Financial Reward + Asset Value
┌──────────────────────────────────────┐   ┌──────────────────────────────────────────┐
│  Miner A Hashrate: 60%  ──► Payoff:  │   │  Network Security Increases              │
│  Miner B Hashrate: 40%  ──► Payoff:  │   │       │                                  │
│                                      │   │       ▼                                  │
│  If Miner A gains +10% hash share:   │   │  Token Value Appreciates ($)             │
│  Miner A Payoff: +0.10 R             │   │       │                                  │
│  Miner B Payoff: -0.10 R             │   │       ▼                                  │
│  Sum of Changes = (+0.10R) + (-0.10R)│   │  Both Miner A & Miner B Gain Higher Real │
│                 = 0                  │   │  World Value (Collective Win)            │
└──────────────────────────────────────┘   └──────────────────────────────────────────┘
```

| Game Theoretic Dimension | Zero-Sum Perspective (Short-Term Block Race) | Non-Zero-Sum Perspective (Long-Term Network Ecosystem) |
| :--- | :--- | :--- |
| **Mathematical Formulation** | $\sum_{i=1}^{m} u_i(s) = C \quad (\Delta u_A = -\Delta u_B)$ | $\sum_{i=1}^{m} u_i(s) = V(\text{Network State}) \neq \text{Constant}$ |
| **Operational Dynamics** | A miner's probability of winning the fixed block subsidy $R$ is proportional to their relative hashrate share: $P_i = \frac{H_i}{\sum H_j}$. Increasing one miner's hash share directly decreases all other miners' expected revenue. | As total computational hash power grows, the blockchain becomes more tamper-resistant, driving higher network adoption, token value, and transaction fee utility. |
| **Attacker Incentives** | An attacker controlling $>51\%$ hashrate could double-spend to maximize short-term extracted value. | Successfully executing a $51\%$ attack crashes public confidence and token price to zero. The attacker destroys their own hardware/capital investments, transforming attack utility from positive to heavily negative. |

---

### Question 5 (10 Marks):
**(a) Compare Public, Private, and Consortium Blockchains across governance, throughput, consensus, and access models.**  
**(b) Explain the specialized Data Structures used in Blockchain: Hash Pointers, Linked Chains, and Ethereum Merkle-Patricia Tries. How do Full, Pruned, and Light nodes perform Information Retrieval?**

---

#### 1. Mumbai University Marking Scheme Rubric (10 Marks)

| Sub-Component | Evaluation Criteria | Allocated Marks |
| :--- | :--- | :--- |
| **Blockchain Platform Taxonomy** | Exhaustive comparative matrix contrasting Public, Private, and Consortium blockchains with practical platform examples. | **3.5 Marks** |
| **Fundamental Data Structures** | Mathematical structure of Hash Pointers, singly linked block chains, and Directed Acyclic Graph (DAG) contrast. | **2 Marks** |
| **Ethereum Merkle-Patricia Tries** | Structural explanation of State Trie, Transaction Trie, Storage Trie, and Receipt Trie; Radix trie and Patricia path compression. | **2.5 Marks** |
| **Information Retrieval Mechanics** | Query pipelines for Full Nodes, Pruned Nodes, SPV Light Nodes, Bloom Filters, and Block Explorer indexing. | **2 Marks** |

---

#### 2. Part (a): Platform Taxonomy: Public vs. Private vs. Consortium Blockchains

Blockchain implementations fall into three primary architectural categories based on participation permissions and governance models:

```
[ PUBLIC BLOCKCHAIN ]          [ CONSORTIUM BLOCKCHAIN ]           [ PRIVATE BLOCKCHAIN ]
 ┌─────────────────┐             ┌─────────────────────┐            ┌──────────────────┐
 │ • Permissionless│             │ • Federated Access  │            │ • Fully Central  │
 │ • Anonymous     │             │ • Known Enterprises │            │ • Single Org     │
 │ • PoW / PoS     │             │ • PBFT / Raft       │            │ • Strict ACLs    │
 │ • Bitcoin / Eth │             │ • Hyperledger/Corda │            │ • Internal Bank  │
 └─────────────────┘             └─────────────────────┘            └──────────────────┘
```

| Architectural Attribute | Public (Permissionless) | Consortium (Federated) | Private (Permissioned) |
| :--- | :--- | :--- | :--- |
| **Access & Read Permissions** | Open to the public; anyone can read, write, and inspect state. | Restricted read/write permissions governed by consortium members. | Strictly internal; access restricted to authorized enterprise users. |
| **Consensus Participants** | Anonymous / Pseudonymous nodes worldwide. | Predetermined set of authorized identity-verified enterprise nodes. | Single central organization or designated internal departments. |
| **Consensus Algorithms** | Proof of Work (PoW), Proof of Stake (PoS) (handles malicious nodes). | Crash Fault Tolerant (CFT) or BFT: Raft, PBFT, Istanbul BFT (IBFT). | Crash Fault Tolerant: Raft, Paxos, or simplified round-robin voting. |
| **Transaction Throughput** | Low to Moderate ($7 - 30$ TPS on Layer-1; scalable via Layer-2). | High ($1,000 - 10,000+$ TPS) due to small, trusted validator sets. | High ($>10,000$ TPS) with low latency. |
| **Energy Consumption** | High (in PoW) to Moderate (in PoS networks). | Negligible; relies on lightweight state-machine messaging rounds. | Negligible; no proof-of-work puzzle competitions. |
| **Incentive Mechanism** | Native cryptocurrency token required for gas fees and block rewards. | Tokens optional; operational costs shared among consortium partners. | No native token required; operational overhead funded internally. |
| **Representative Platforms** | Bitcoin, Ethereum, Solana, Cardano. | Hyperledger Fabric, R3 Corda, Quorum. | Multichain, Hyperledger Besu (Private Mode). |

---

#### 3. Part (b): Specialized Blockchain Data Structures and Information Retrieval

##### 1. Hash Pointers and Hash Chains
A **Hash Pointer** is a two-component data structure that stores:
1. A memory pointer or disk address reference to the target data block: $p$.
2. The cryptographic hash digest of the data stored inside that target block: $H(\text{Data})$.

$$\text{HashPointer} = (p, H(\text{Data}))$$

In a standard linked list, pointers indicate *where* data is stored. In a **Hash Chain**, hash pointers indicate both *where* the data resides and verify that the data has not been modified. If an attacker tampers with data at pointer $p$, the recomputed hash $\text{SHA256}(\text{Data}')$ will not match the stored hash digest $H(\text{Data})$, immediately exposing the tampering.

```
       Block N-1                          Block N                          Block N+1
┌──────────────────────┐           ┌──────────────────────┐          ┌──────────────────────┐
│ Data: [Tx Payload]   │           │ Data: [Tx Payload]   │          │ Data: [Tx Payload]   │
├──────────────────────┤           ├──────────────────────┤          ├──────────────────────┤
│ PrevHashPointer:     │◄──────────┤ PrevHashPointer:     │◄─────────┤ PrevHashPointer:     │
│ [Addr N-2, H(Blk N-2)]│           │ [Addr N-1, H(Blk N-1)]│          │ [Addr N, H(Blk N)]   │
└──────────────────────┘           └──────────────────────┘          └──────────────────────┘
```

---

##### 2. Ethereum Merkle-Patricia Tries (MPT)
While Bitcoin utilizes simple binary Merkle trees for transactions, Ethereum uses a more sophisticated structure: the **Modified Merkle-Patricia Trie (MPT)**. This combines a deterministic **Radix Trie** with **Patricia Path Compression** and cryptographic hash pointers to efficiently track state changes.

Ethereum maintains four independent trie roots inside each block header:
1. **State Trie**: Maps 20-byte account addresses to account states (nonce, balance, storageRoot, codeHash). Updated dynamically with each transaction.
2. **Storage Trie**: Houses contract storage variables as a persistent key-value trie linked into the State Trie via `storageRoot`.
3. **Transaction Trie**: Records all transactions in the current block, indexed by their RLP-encoded transaction sequence position.
4. **Receipt Trie**: Records transaction execution receipts, post-transaction state roots, cumulative gas consumption, and emitted event logs.

```
                  [ Block Header State Root ]
                               │
                               ▼
                    [ MPT Root Hash Node ]
                   ┌───────────┴───────────┐
                   ▼                       ▼
            [ Branch Node ]         [ Extension Node ]
            (16 Hex Nibbles)        (Shared Key Path)
                   │                       │
                   ▼                       ▼
             [ Leaf Node ]           [ Leaf Node ]
             (Account State)         (Account State)
```

###### MPT Node Types:
* **Null Node**: Represents an empty item.
* **Branch Node**: A 17-element array: sixteen 4-bit hex nibble pointers $[0\text{--}f]$ leading to child nodes, plus a 17th element for value storage.
* **Extension Node**: A 2-item node `[encodedPath, childHash]` that compresses shared path segments, avoiding redundant empty branch nodes.
* **Leaf Node**: A 2-item node `[encodedPath, value]` representing terminating key-value records.

---

##### 3. Information Retrieval Architecture Across Node Types

Distributed ledger networks deploy multiple node topologies to balance storage capacity, compute overhead, and query performance:

```
[ RPC Client / DApp Query ]
             │
             ├──► [ Full Node ]: Reads local RocksDB / LevelDB ──► Instantaneous (All Historical Blocks)
             │
             ├──► [ Pruned Node ]: Reads recent blocks (e.g., last 550 blocks) ──► Validates recent states
             │
             └──► [ SPV Light Node ]: Issues Bloom Filter / Merkle Path Request to Full Node Peer
                                      │
                                      ▼
                        Full Node returns Merkle Proof ──► Light Node verifies H(Tx) against Header
```

1. **Full Archival Nodes**:
   * Download and validate every transaction, block header, and state update from the Genesis block to the tip of the chain.
   * Store the full state trie in local key-value databases (LevelDB or RocksDB).
   * Resolve queries instantaneously without relying on external network peers.
2. **Pruned Full Nodes**:
   * Fully validate all blocks from Genesis, but delete historical block bodies and state snapshots older than a specified depth (e.g., retaining only the most recent 550 blocks).
   * Maintain the full current state database, enabling transaction execution and validation while using less disk space ($\sim 15\text{ GB}$).
3. **SPV Light Nodes (Bloom Filter Retrieval)**:
   * Store only block headers. To check account balances or transaction confirmations without leaking wallet addresses, the light client sends a **Bloom Filter** (a space-efficient probabilistic data structure using multiple hash functions) to connected full nodes.
   * Full nodes scan blocks against the bloom filter and return matching transactions alongside their $O(\log_2 N)$ Merkle audit paths.
4. **Block Explorers & Indexing Services**:
   * Platforms like Etherscan utilize specialized ingestion daemons to stream block events from full node RPC endpoints (JSON-RPC) into relational databases (PostgreSQL) and search indices (Elasticsearch), providing sub-second search indexing by address, transaction hash, block height, and timestamp.

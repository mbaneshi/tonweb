block storage

It looks like you've provided TypeScript code for block definitions and an interface related to shardchains and block storage. Let's break down the key components:

1. **ShardBlock Interface:**
   - `ShardBlock` is an interface representing a shardchain block.
   - It has three properties:
     - `workchain` (a number): Represents the workchain associated with the shard.
     - `shardId` (a string): Represents the identifier of the shard.
     - `shardBlockNumber` (a number): Represents the block number within the shard.

2. **BlockStorage Interface:**
   - `BlockStorage` is an interface defining functions related to block storage and retrieval.
   - `insertBlocks`: Inserts new processed masterchain block number and unprocessed shardchain block numbers. This function takes a masterchain block number (`mcBlockNumber`) and an array of `ShardBlock` objects (`shardBlocks`). It returns a Promise that resolves once the insertion is complete.
   - `getLastMasterchainBlockNumber`: Returns the last processed masterchain block number. It returns a Promise that resolves to either a number or `undefined`.
   - `setBlockProcessed`: Marks a specified shardchain block as processed and inserts new unprocessed shardchain block numbers. It takes the workchain, shard ID, shard block number, and an array of previous shard blocks (`prevShardBlocks`). It returns a Promise that resolves once the operation is complete.
   - `getUnprocessedShardBlock`: Returns any unprocessed shard block numbers. It returns a Promise that resolves to either a `ShardBlock` object or `undefined`.

These interfaces seem to be part of a larger system or library for handling shardchain blocks and their storage. The code structure suggests that it may be used in a blockchain or distributed ledger system where different chains (masterchain and shardchain) are being processed and stored.

If you have specific questions or if there's anything specific you'd like to know or discuss about this code, feel free to ask!

***

block subscription

This TypeScript code defines a `BlockSubscription` class, which appears to be part of a system for subscribing to and processing blocks in a blockchain or distributed ledger. Let's break down the key components:

1. **Import Statements:**
   - It imports the `HttpProvider` from the '../http-provider' module and the `BlockStorage` from the './block-storage' module.

2. **BlockSubscriptionOptions Interface:**
   - It defines an interface `BlockSubscriptionOptions` that represents the options for configuring a block subscription.
   - Options include:
      - `startMcBlockNumber`: The starting masterchain block number for processing blocks.
      - `mcInterval`: The interval for masterchain block processing.
      - `shardsInterval`: The interval for shardchain block processing.

3. **BlockHandler Type:**
   - It defines a type `BlockHandler` for the callback function that will be called for each block. The callback takes a `blockHeader` and an optional `blockShards` parameter and returns a `Promise<void>` or `void`.

4. **BlockSubscription Class:**
   - It declares a class `BlockSubscription` that represents a subscription to block events.
   - Constructor Parameters:
      - `provider`: An instance of the TonWeb HTTP provider (`HttpProvider`).
      - `storage`: An instance of the persistent storage for storing processed block numbers (`BlockStorage`).
      - `onBlock`: The callback function to be called for each block (`BlockHandler`).
      - `options`: Optional configuration options for the subscription (`BlockSubscriptionOptions`).
   - Class Properties:
      - `provider`: TonWeb HTTP provider.
      - `storage`: Persistent storage for processed block numbers.
      - `onBlock`: Callback function for block processing.
      - `options`: Configuration options for the subscription.
      - `startMcBlockNumber`: The starting masterchain block number.
      - `mcInterval`: The interval for masterchain block processing.
      - `shardsInterval`: The interval for shardchain block processing.
      - `startLT`: Start logical time for block processing.
      - `mcIntervalId`, `shardsIntervalId`: Interval IDs for masterchain and shardchain processing.
   - Class Methods:
      - `start()`: Starts the block subscription. Returns a Promise that resolves when the subscription is started.
      - `stop()`: Stops the block subscription.

This class seems to manage the subscription to block events, with the ability to start and stop the subscription, and it provides a callback function (`onBlock`) for processing each block. The class uses a TonWeb HTTP provider for communication and a persistent storage mechanism for storing processed block numbers.

If you have specific questions or if there's anything specific you'd like to know or discuss about this code, feel free to ask!


***

in memory block storage 
This TypeScript code defines an `InMemoryBlockStorage` class, which is a simple in-memory implementation of a block storage mechanism for processed block numbers. Let's break down the key components:

1. **Import Statements:**
   - It imports `BlockStorage` and `ShardBlock` from './block-storage'.

2. **LogFunction Type:**
   - It defines a type `LogFunction` for a function that logs a message. The function takes a `message` (string) parameter and returns `void`.

3. **InMemoryBlockStorage Class:**
   - It declares a class `InMemoryBlockStorage` representing an in-memory block storage implementation.
   - Constructor Parameters:
      - `logFunction`: A function for logging messages.
   - Class Properties:
      - `logFunction`: The log function provided during instantiation.
      - `masterBlocks`: A map of processed masterchain blocks. The keys are block numbers, and values indicate the processed state.
      - `shardBlocks`: A map of processed shardchain blocks. The keys are constructed using the format `${workchain}_${shardId}_${shardBlockNumber}`, and values indicate the processed state.
   - Class Methods:
      - `insertBlocks(mcBlockNumber: number, shardBlockNumbers: ShardBlock[]): Promise<void>`: Inserts new processed masterchain block number and unprocessed shardchain block numbers. It returns a Promise that resolves when the insertion is complete.
      - `getLastMasterchainBlockNumber(): Promise<number | undefined>`: Returns the last processed masterchain block number. It returns a Promise that resolves to either a number or `undefined`.
      - `setBlockProcessed(workchain: number, shardId: string, shardBlockNumber: number, prevShardBlocks: ShardBlock[]): Promise<void>`: Marks the specified shardchain block number as processed and inserts new unprocessed shardchain block numbers. It returns a Promise that resolves when the operation is complete.
      - `getUnprocessedShardBlock(): Promise<ShardBlock | undefined>`: Returns any unprocessed shard block numbers. It returns a Promise that resolves to either a `ShardBlock` object or `undefined`.
      - `insertShardBlocks(shardBlockNumbers: ShardBlock[]): void`: Inserts new unprocessed shardchain block numbers. Block numbers should be ignored if they are already in the storage.
      - `getShardBlockKey(workchain: number, shardId: string, shardBlockNumber: number): string`: Generates a unique key for identifying a specified shardchain block.
      - `parseShardBlockKey(key: string): ShardBlock`: Parses a specified shardchain block key and returns a `ShardBlock` definition.

The class provides a simple in-memory storage solution for processed block numbers, supporting masterchain and shardchain blocks. It uses maps for both masterchain and shardchain blocks, and it includes methods for insertion, retrieval, and processing of blocks.

If you have specific questions or if there's anything specific you'd like to know or discuss about this code, feel free to ask!

***

sql block storage 

This TypeScript code defines a `SqlBlockStorage` class, which is described as a proof of concept for an RDBMS (SQL) shardchain block storage implementation. However, the implementation lacks details and the actual SQL operations needed for the specified methods. Let's go through the key components:

1. **Import Statement:**
   - It imports `BlockStorage` and `ShardBlock` from './block-storage'.

2. **SqlBlockStorage Class:**
   - It declares a class `SqlBlockStorage` that is intended to be an RDBMS-based implementation of the `BlockStorage` interface.
   - Class Methods:
      - `insertBlocks(mcBlockNumber: number, shardBlockNumbers: ShardBlock[]): Promise<void>`: Inserts new processed masterchain block number and unprocessed shardchain block numbers into the SQL storage. The implementation of this method is not provided in the code snippet.
      - `getLastMasterchainBlockNumber(): Promise<number | undefined>`: Retrieves the last processed masterchain block number from the SQL storage. The implementation details are missing.
      - `setBlockProcessed(workchain: number, shardId: string, shardBlockNumber: number, prevShardBlocks: ShardBlock[]): Promise<void>`: Marks the specified shardchain block number as processed in the SQL storage and inserts new unprocessed shardchain block numbers. The actual SQL operations are not defined in the code snippet.
      - `getUnprocessedShardBlock(): Promise<ShardBlock | undefined>`: Retrieves any unprocessed shard block numbers from the SQL storage. The implementation details for SQL queries are not provided.

**Note:** The class declaration is essentially an interface without a concrete implementation. In a real-world scenario, you would need to implement the actual SQL queries, connections, and operations within each of these methods to interact with an SQL database.

If you are planning to use an SQL database for storing block data, you would typically use a library like Knex.js or Sequelize to interact with the database, and you'd define SQL queries within these methods to perform the required operations.

If you have a specific SQL database in mind or if you need assistance with implementing SQL queries for these methods, please provide more details so that I can offer more targeted guidance.



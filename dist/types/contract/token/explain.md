[Link](https://chat.openai.com/c/7d0803c3-0abe-42ba-b687-4e802e333f0a)


jetton-minter.d.ts.md
This TypeScript code defines a class named `JettonMinter` that extends another class `Contract`. Let's break down the key elements:

1. **Imports:**
   ```typescript
   import BN from 'bn.js';
   import { Cell } from '../../../boc/cell';
   import { HttpProvider } from '../../../providers/http-provider';
   import { Address } from '../../../utils/address';
   import { Contract, ContractMethods, ContractOptions } from '../../contract';
   ```

   These are import statements bringing in necessary dependencies and classes from other modules.

2. **Interfaces:**
   ```typescript
   export interface JettonMinterOptions extends ContractOptions {
       wc?: 0;
       adminAddress: Address;
       jettonContentUri: string;
       jettonWalletCodeHex: string;
   }
   ```

   This interface `JettonMinterOptions` extends another interface `ContractOptions` and adds some specific properties.

   ```typescript
   export interface MintBodyParams {
       tokenAmount: BN;
       destination: Address;
       amount: BN;
       queryId?: number;
   }
   ```

   This is an interface `MintBodyParams` that defines the parameters for the `createMintBody` method.

   ```typescript
   export interface JettonData {
       totalSupply: BN;
       isMutable: boolean;
       jettonContentUri: string;
       tokenWalletCode: Cell;
       adminAddress?: Address;
   }
   ```

   This is an interface `JettonData` representing data related to the `JettonMinter` class.

3. **Class Definition:**
   ```typescript
   export declare class JettonMinter extends Contract<JettonMinterOptions, JettonMinterMethods> {
       // ... constructor and methods ...
   }
   ```

   The `JettonMinter` class extends `Contract` and specifies the generic types `JettonMinterOptions` and `JettonMinterMethods`.

4. **Constructor:**
   ```typescript
   constructor(provider: HttpProvider, options: JettonMinterOptions) {
       super(provider, options);
   }
   ```

   The constructor takes a `HttpProvider` and some `options`, then calls the constructor of the parent class `Contract` using `super`.

5. **Additional Methods:**
   ```typescript
   createMintBody(params: MintBodyParams): Cell;
   getJettonData(): Promise<JettonData>;
   getJettonWalletAddress(ownerAddress: Address): Promise<Address>;
   ```

   These methods appear to provide functionality related to creating a mint body, retrieving jetton data, and getting the jetton wallet address.

6. **Protected Method:**
   ```typescript
   protected createDataCell(): Cell;
   ```

   This protected method is meant to be used internally within the class for creating a cell that contains jetton minter data.

Overall, it looks like this class is part of a larger system related to a jetton minter, possibly in the context of a blockchain or cryptocurrency project. The class has methods for creating mint bodies, retrieving data, and managing jetton wallets. If you have specific questions about parts of the code or if you need help with something specific, feel free to ask!

***

jetton-wallet.d.ts.md

This TypeScript code defines a class named `JettonWallet` that extends another class `Contract`. Similar to the previous examples, let's break down the key elements:

1. **Imports:**
   ```typescript
   import BN from 'bn.js';
   import { Cell } from '../../../boc/cell';
   import { HttpProvider } from '../../../providers/http-provider';
   import { Address } from '../../../utils/address';
   import { Contract, ContractMethods, ContractOptions } from '../../contract';
   ```

   These are import statements bringing in necessary dependencies and classes from other modules.

2. **Interfaces:**
   ```typescript
   export interface JettonWalletOptions extends ContractOptions {
       wc?: 0;
   }
   ```

   This interface `JettonWalletOptions` extends another interface `ContractOptions` and adds some specific properties.

   ```typescript
   export interface WalletData {
       balance: BN;
       ownerAddress: Address;
       jettonMinterAddress: Address;
       tokenWalletCode: Cell;
   }
   ```

   This is an interface `WalletData` representing data related to the `JettonWallet` class.

   ```typescript
   export interface TransferBodyParams {
       queryId?: number;
       tokenAmount: BN;
       toAddress: Address;
       responseAddress: Address;
       forwardAmount: BN;
       forwardPayload: Uint8Array;
   }
   ```

   This is an interface `TransferBodyParams` defining parameters for the `createTransferBody` method.

   ```typescript
   export interface BurnBodyParams {
       queryId?: number;
       tokenAmount: BN;
       responseAddress: Address;
   }
   ```

   This is an interface `BurnBodyParams` defining parameters for the `createBurnBody` method.

3. **Class Definition:**
   ```typescript
   export declare class JettonWallet extends Contract<JettonWalletOptions, JettonWalletMethods> {
       // ... constructor and methods ...
   }
   ```

   The `JettonWallet` class extends `Contract` and specifies the generic types `JettonWalletOptions` and `JettonWalletMethods`.

4. **Static Property:**
   ```typescript
   static codeHex: string;
   ```

   This static property `codeHex` is a string and seems to represent the hexadecimal code associated with the `JettonWallet` class.

5. **Constructor:**
   ```typescript
   constructor(provider: HttpProvider, options: JettonWalletOptions) {
       super(provider, options);
   }
   ```

   The constructor takes a `HttpProvider` and some `options`, then calls the constructor of the parent class `Contract` using `super`.

6. **Additional Methods:**
   ```typescript
   getData(): Promise<WalletData>;
   createTransferBody(params: TransferBodyParams): Promise<Cell>;
   createBurnBody(params: BurnBodyParams): Promise<Cell>;
   ```

   These methods appear to provide functionality related to getting wallet data, creating transfer bodies, and creating burn bodies.

Overall, it seems like this class is part of a larger system related to a jetton wallet, possibly in the context of a blockchain or cryptocurrency project. The class has methods for interacting with wallet data, creating transfer bodies, and creating burn bodies. If you have specific questions about parts of the code or if you need help with something specific, feel free to ask!


***


This TypeScript code defines a class named `NftCollection` that extends another class `Contract`. Let's break down the key elements:

1. **Imports:**
   ```typescript
   import BN from 'bn.js';
   import { Cell } from '../../../boc/cell';
   import { HttpProvider } from '../../../providers/http-provider';
   import { Address } from '../../../utils/address';
   import { Contract, ContractMethods, ContractOptions } from '../../contract';
   import { NftItem } from './nft-item';
   ```

   These are import statements bringing in necessary dependencies and classes from other modules, including `NftItem` from the same directory.

2. **Interfaces:**
   ```typescript
   export interface NftCollectionOptions extends ContractOptions {
       ownerAddress?: Address;
       collectionContentUri?: string;
       nftItemContentBaseUri?: string;
       nftItemCodeHex?: string;
       royalty?: number;
       royaltyAddress?: Address;
   }
   ```

   This interface `NftCollectionOptions` extends another interface `ContractOptions` and adds some specific properties.

   ```typescript
   export interface NftCollectionMethods extends ContractMethods {
       // ... method signatures ...
   }
   ```

   This is an interface `NftCollectionMethods` defining method signatures for the `NftCollection` class.

   ```typescript
   export interface MintBodyParams {
       // ... parameters ...
   }
   ```

   This is an interface `MintBodyParams` defining parameters for the `createMintBody` method.

   ```typescript
   export interface CreateGetRoyaltyParamsBodyParams {
       // ... parameters ...
   }
   ```

   This is an interface `CreateGetRoyaltyParamsBodyParams` defining parameters for the `createGetRoyaltyParamsBody` method.

   ```typescript
   export interface CreateChangeOwnerBodyParams {
       // ... parameters ...
   }
   ```

   This is an interface `CreateChangeOwnerBodyParams` defining parameters for the `createChangeOwnerBody` method.

   ```typescript
   export interface CollectionData {
       // ... properties ...
   }
   ```

   This is an interface `CollectionData` representing data related to the `NftCollection` class.

   ```typescript
   export interface NftItemContent {
       // ... properties ...
   }
   ```

   This is an interface `NftItemContent` representing content related to an NFT item.

   ```typescript
   export interface RoyaltyParams {
       // ... properties ...
   }
   ```

   This is an interface `RoyaltyParams` representing royalty-related parameters.

3. **Class Definition:**
   ```typescript
   export declare class NftCollection extends Contract<NftCollectionOptions, NftCollectionMethods> {
       // ... constructor and methods ...
   }
   ```

   The `NftCollection` class extends `Contract` and specifies the generic types `NftCollectionOptions` and `NftCollectionMethods`.

4. **Constants:**
   ```typescript
   private readonly royaltyBase;
   private readonly royaltyFactor;
   ```

   These are private constants used within the class.

5. **Constructor:**
   ```typescript
   constructor(provider: HttpProvider, options: NftCollectionOptions) {
       super(provider, options);
   }
   ```

   The constructor takes a `HttpProvider` and some `options`, then calls the constructor of the parent class `Contract` using `super`.

6. **Additional Methods:**
   ```typescript
   createMintBody(params: MintBodyParams): Cell;
   createGetRoyaltyParamsBody(params: CreateGetRoyaltyParamsBodyParams): Cell;
   createChangeOwnerBody(params: CreateChangeOwnerBodyParams): Cell;
   getCollectionData(): Promise<CollectionData>;
   getNftItemContent(nftItem: NftItem): Promise<NftItemContent>;
   getNftItemAddressByIndex(index: number): Promise<Address>;
   getRoyaltyParams(): Promise<RoyaltyParams>;
   ```

   These methods provide functionality related to creating mint bodies, retrieving collection data, getting NFT item content, and handling royalties.

7. **Protected Method:**
   ```typescript
   protected createDataCell(): Cell;
   ```

   This protected method is meant to be used internally within the class for creating a cell that contains NFT collection data.

Overall, it appears that this class is part of a larger system related to NFTs (Non-Fungible Tokens), possibly in the context of a blockchain or cryptocurrency project. The class has methods for creating NFT-related bodies, retrieving data, and managing royalties. If you have specific questions about parts of the code or if you need help with something specific, feel free to ask!


****


nft-item

This TypeScript code defines a class named `NftItem` that extends another class `Contract`. Let's break down the key elements:

1. **Imports:**
   ```typescript
   import BN from 'bn.js';
   import { Cell } from '../../../boc/cell';
   import { HttpProvider } from '../../../providers/http-provider';
   import { Address } from '../../../utils/address';
   import { Contract, ContractMethods, ContractOptions } from '../../contract';
   ```

   These are import statements bringing in necessary dependencies and classes from other modules.

2. **Interfaces:**
   ```typescript
   export interface NftItemOptions extends ContractOptions {
       index?: number;
       collectionAddress?: Address;
   }
   ```

   This interface `NftItemOptions` extends another interface `ContractOptions` and adds some specific properties.

   ```typescript
   export interface NftItemMethods extends ContractMethods {
       getData: () => Promise<NftItemData>;
   }
   ```

   This is an interface `NftItemMethods` defining method signatures for the `NftItem` class.

   ```typescript
   export interface NftItemData {
       isInitialized: boolean;
       index: number;
       collectionAddress: Address;
       contentCell: Cell;
       ownerAddress?: Address;
   }
   ```

   This is an interface `NftItemData` representing data related to the `NftItem` class.

   ```typescript
   export interface CreateTransferBodyParams {
       // ... parameters ...
   }
   ```

   This is an interface `CreateTransferBodyParams` defining parameters for the `createTransferBody` method.

   ```typescript
   export interface CreateGetStaticDataBodyParams {
       // ... parameters ...
   }
   ```

   This is an interface `CreateGetStaticDataBodyParams` defining parameters for the `createGetStaticDataBody` method.

3. **Class Definition:**
   ```typescript
   export declare class NftItem extends Contract<NftItemOptions, NftItemMethods> {
       // ... constructor and methods ...
   }
   ```

   The `NftItem` class extends `Contract` and specifies the generic types `NftItemOptions` and `NftItemMethods`.

4. **Static Property:**
   ```typescript
   static codeHex: string;
   ```

   This static property `codeHex` is a string and seems to represent the hexadecimal code associated with the `NftItem` class.

5. **Constructor:**
   ```typescript
   constructor(provider: HttpProvider, options: NftItemOptions) {
       super(provider, options);
   }
   ```

   The constructor takes a `HttpProvider` and some `options`, then calls the constructor of the parent class `Contract` using `super`.

6. **Additional Methods:**
   ```typescript
   getData(): Promise<NftItemData>;
   createTransferBody(params: CreateTransferBodyParams): Promise<Cell>;
   createGetStaticDataBody(params: CreateGetStaticDataBodyParams): Cell;
   ```

   These methods provide functionality related to getting NFT item data, creating transfer bodies, and getting static data.

7. **Protected Method:**
   ```typescript
   protected createDataCell(): Cell;
   ```

   This protected method is meant to be used internally within the class for creating a cell that contains NFT item data.

Overall, it appears that this class is part of a larger system related to NFTs (Non-Fungible Tokens), possibly in the context of a blockchain or cryptocurrency project. The class has methods for interacting with NFT item data, creating transfer bodies, and obtaining static data. If you have specific questions about parts of the code or if you need help with something specific, feel free to ask!


****

Nft sale

This TypeScript code defines a class named `NftSale` that extends another class `Contract`. Let's break down the key elements:

1. **Imports:**
   ```typescript
   import BN from 'bn.js';
   import { Cell } from '../../../boc/cell';
   import { HttpProvider } from '../../../providers/http-provider';
   import { Address } from '../../../utils/address';
   import { Contract, ContractMethods, ContractOptions } from '../../contract';
   ```

   These are import statements bringing in necessary dependencies and classes from other modules.

2. **Interfaces:**
   ```typescript
   export interface NftSaleOptions extends ContractOptions {
       marketplaceAddress?: Address;
       nftAddress?: Address;
       fullPrice?: BN;
       marketplaceFee?: BN;
       royaltyAddress?: Address;
       royaltyAmount?: BN;
   }
   ```

   This interface `NftSaleOptions` extends another interface `ContractOptions` and adds some specific properties.

   ```typescript
   export interface NftSaleMethods extends ContractMethods {
       getData: () => Promise<NftSaleData>;
   }
   ```

   This is an interface `NftSaleMethods` defining method signatures for the `NftSale` class.

   ```typescript
   export interface NftSaleData {
       // ... properties ...
   }
   ```

   This is an interface `NftSaleData` representing data related to the `NftSale` class.

   ```typescript
   export interface CreateCancelBodyParams {
       // ... parameters ...
   }
   ```

   This is an interface `CreateCancelBodyParams` defining parameters for the `createCancelBody` method.

3. **Class Definition:**
   ```typescript
   export declare class NftSale extends Contract<NftSaleOptions, NftSaleMethods> {
       // ... constructor and methods ...
   }
   ```

   The `NftSale` class extends `Contract` and specifies the generic types `NftSaleOptions` and `NftSaleMethods`.

4. **Static Property:**
   ```typescript
   static codeHex: string;
   ```

   This static property `codeHex` is a string and seems to represent the hexadecimal code associated with the `NftSale` class.

5. **Constructor:**
   ```typescript
   constructor(provider: HttpProvider, options: NftSaleOptions) {
       super(provider, options);
   }
   ```

   The constructor takes a `HttpProvider` and some `options`, then calls the constructor of the parent class `Contract` using `super`.

6. **Additional Methods:**
   ```typescript
   getData(): Promise<NftSaleData>;
   createCancelBody(params: CreateCancelBodyParams): Promise<Cell>;
   ```

   These methods provide functionality related to getting NFT sale data and creating cancel bodies.

7. **Protected Method:**
   ```typescript
   protected createDataCell(): Cell;
   ```

   This protected method is meant to be used internally within the class for creating a cell that contains NFT sale data.

Overall, it appears that this class is part of a larger system related to NFT sales, possibly in the context of a marketplace or platform for trading NFTs. The class has methods for interacting with sale data and creating cancel bodies. If you have specific questions about parts of the code or if you need help with something specific, feel free to ask!


***


util

This TypeScript code appears to define some constants and functions related to handling data serialization and parsing, specifically for URIs and addresses. Let's break down the key elements:

1. **Constants:**
   ```typescript
   export const SNAKE_DATA_PREFIX = 0;
   export const CHUNK_DATA_PREFIX = 1;
   export const ONCHAIN_CONTENT_PREFIX = 0;
   export const OFFCHAIN_CONTENT_PREFIX = 1;
   ```

   These are constant values representing prefixes for different types of data or content. For example, `SNAKE_DATA_PREFIX` and `CHUNK_DATA_PREFIX` may be used to distinguish between different types of data.

2. **Functions:**
   ```typescript
   export declare function serializeUri(uri: string): Uint8Array;
   ```

   This function `serializeUri` takes a string `uri` and returns a `Uint8Array`. It seems to be responsible for converting a URI string into a serialized binary format.

   ```typescript
   export declare function parseUri(bytes: Uint8Array): string;
   ```

   This function `parseUri` takes a `Uint8Array` of bytes and returns a string. It appears to be the reverse of `serializeUri`, converting the serialized binary data back into a URI string.

   ```typescript
   export declare function createOffchainUriCell(uri: string): Cell;
   ```

   This function `createOffchainUriCell` takes a URI string and returns a `Cell`. It seems to be creating a cell, possibly for off-chain data storage, based on the provided URI.

   ```typescript
   export declare function parseOffchainUriCell(cell: Cell): string;
   ```

   This function `parseOffchainUriCell` takes a `Cell` and returns a string. It appears to be extracting and parsing a URI from an off-chain cell.

   ```typescript
   export declare function parseAddress(cell: Cell): (Address | undefined);
   ```

   This function `parseAddress` takes a `Cell` and returns either an `Address` or `undefined`. It is likely used to parse an address from the given cell.

Overall, these functions and constants suggest that the code is dealing with serialization and parsing of URIs and addresses, and there are specific considerations for different types of data or content, such as on-chain and off-chain content. If you have specific questions about how to use these functions or need further clarification on any part, feel free to ask!



***


***

ft

This TypeScript code defines a class named `JettonMinter` that extends another class `Contract`. Let's break down the key elements:

1. **Imports:**
   ```typescript
   import BN from 'bn.js';
   import { Cell } from '../../../boc/cell';
   import { HttpProvider } from '../../../providers/http-provider';
   import { Address } from '../../../utils/address';
   import { Contract, ContractMethods, ContractOptions } from '../../contract';
   ```

   These are import statements bringing in necessary dependencies and classes from other modules.

2. **Interfaces:**
   ```typescript
   export interface JettonMinterOptions extends ContractOptions {
       wc?: 0;
       adminAddress: Address;
       jettonContentUri: string;
       jettonWalletCodeHex: string;
   }
   ```

   This interface `JettonMinterOptions` extends another interface `ContractOptions` and adds some specific properties.

   ```typescript
   export interface JettonMinterMethods extends ContractMethods {
       // ... method signatures ...
   }
   ```

   This is an interface `JettonMinterMethods` defining method signatures for the `JettonMinter` class.

   ```typescript
   export interface MintBodyParams {
       // ... parameters ...
   }
   ```

   This is an interface `MintBodyParams` defining parameters for the `createMintBody` method.

   ```typescript
   export interface JettonData {
       // ... properties ...
   }
   ```

   This is an interface `JettonData` representing data related to the `JettonMinter` class.

3. **Class Definition:**
   ```typescript
   export declare class JettonMinter extends Contract<JettonMinterOptions, JettonMinterMethods> {
       // ... constructor and methods ...
   }
   ```

   The `JettonMinter` class extends `Contract` and specifies the generic types `JettonMinterOptions` and `JettonMinterMethods`.

4. **Constructor:**
   ```typescript
   constructor(provider: HttpProvider, options: JettonMinterOptions) {
       super(provider, options);
   }
   ```

   The constructor takes a `HttpProvider` and some `options`, then calls the constructor of the parent class `Contract` using `super`.

5. **Additional Methods:**
   ```typescript
   createMintBody(params: MintBodyParams): Cell;
   getJettonData(): Promise<JettonData>;
   getJettonWalletAddress(ownerAddress: Address): Promise<Address>;
   ```

   These methods provide functionality related to creating mint bodies, retrieving jetton data, and getting the jetton wallet address.

6. **Protected Method:**
   ```typescript
   protected createDataCell(): Cell;
   ```

   This protected method is meant to be used internally within the class for creating a cell that contains jetton minter data.

The class appears to be part of a larger system related to a jetton minter, possibly in the context of a blockchain or cryptocurrency project. The class has methods for creating mint bodies, retrieving data, and managing jetton wallets. If you have specific questions about parts of the code or if you need help with something specific, feel free to ask!


***

This TypeScript code defines a class named `JettonWallet` that extends another class `Contract`. Let's break down the key elements:

1. **Imports:**
   ```typescript
   import BN from 'bn.js';
   import { Cell } from '../../../boc/cell';
   import { HttpProvider } from '../../../providers/http-provider';
   import { Address } from '../../../utils/address';
   import { Contract, ContractMethods, ContractOptions } from '../../contract';
   ```

   These are import statements bringing in necessary dependencies and classes from other modules.

2. **Interfaces:**
   ```typescript
   export interface JettonWalletOptions extends ContractOptions {
       wc?: 0;
   }
   ```

   This interface `JettonWalletOptions` extends another interface `ContractOptions` and adds a specific property.

   ```typescript
   export interface JettonWalletMethods extends ContractMethods {
       // ... method signatures ...
   }
   ```

   This is an interface `JettonWalletMethods` defining method signatures for the `JettonWallet` class.

   ```typescript
   export interface WalletData {
       // ... properties ...
   }
   ```

   This is an interface `WalletData` representing data related to the `JettonWallet` class.

   ```typescript
   export interface TransferBodyParams {
       // ... parameters ...
   }
   ```

   This is an interface `TransferBodyParams` defining parameters for the `createTransferBody` method.

   ```typescript
   export interface BurnBodyParams {
       // ... parameters ...
   }
   ```

   This is an interface `BurnBodyParams` defining parameters for the `createBurnBody` method.

3. **Class Definition:**
   ```typescript
   export declare class JettonWallet extends Contract<JettonWalletOptions, JettonWalletMethods> {
       // ... constructor and methods ...
   }
   ```

   The `JettonWallet` class extends `Contract` and specifies the generic types `JettonWalletOptions` and `JettonWalletMethods`.

4. **Static Property:**
   ```typescript
   static codeHex: string;
   ```

   This static property `codeHex` is a string and seems to represent the hexadecimal code associated with the `JettonWallet` class.

5. **Constructor:**
   ```typescript
   constructor(provider: HttpProvider, options: JettonWalletOptions) {
       super(provider, options);
   }
   ```

   The constructor takes a `HttpProvider` and some `options`, then calls the constructor of the parent class `Contract` using `super`.

6. **Additional Methods:**
   ```typescript
   getData(): Promise<WalletData>;
   createTransferBody(params: TransferBodyParams): Promise<Cell>;
   createBurnBody(params: BurnBodyParams): Promise<Cell>;
   ```

   These methods provide functionality related to getting wallet data, creating transfer bodies, and creating burn bodies.

The class appears to be part of a larger system related to jetton wallets, possibly in the context of a blockchain or cryptocurrency project. The class has methods for interacting with wallet data, creating transfer bodies, and creating burn bodies. If you have specific questions about parts of the code or if you need help with something specific, feel free to ask!



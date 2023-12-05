# Getting a Quote

## Introduction
This guide will cover how to get the current quotes for any token pair in ICPSwap. 
Before starting, try to get the id of ICP - SNS1 SwapPool canister by [Searching a Pool](../../SwapFactory/Searching%20a%20Pool.md). 

In this example we will use **quote** to get a quote for the pair ICP - SNS1. The inputs are the *zeroForOne* symbol, the *amountIn* and the *amountOutMinimum*.

For this guide, the following canister ids are used:
|Name|Principal|
|:-|:-:|
|SwapFactory|4mmnk-kiaaa-aaaag-qbllq-cai|
|SwapPool of ICP - SNS1|3ejs3-eaaaa-aaaag-qbl2a-cai|

## Command
By the output data of [Searching a Pool](../Factory/Searching%20a%20Pool.md), we can see that in the SwapPool of pair ICP - SNS1, the token0 is ICP, and the token1 is SNS1. 

```
dfx canister --network=ic call 3ejs3-eaaaa-aaaag-qbl2a-cai quote '(record { zeroForOne = true; amountIn = "100000000"; amountOutMinimum = "0"; })'
```

## Detail

did
```
type Result = variant { ok : nat; err : Error };

type SwapArgs = record {
  amountIn : text;
  zeroForOne : bool;
  amountOutMinimum : text;
};

type SwapPool = service {
    quote : (SwapArgs) -> (Result) query;
}

service : SwapPool
```
In the input parameters:
+ *zeroForOne* is the symbol for trading direction. If token0 swaps token1, then *true*, otherwise *false*.
+ *amountIn* is amount of input token.
+ *amountOutMinimum* is the expected minimum amount of output token. Used as a sliding point restriction in **swap** function, but 0 is ok here.
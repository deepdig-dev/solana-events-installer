## Abount
This repository serves as an additional documentation for the Solana Events API project. Here, we will demonstrate how to read Solana data, store the data in a database, and provide simple query solutions for use cases.  

本仓库是作为 Solana Events API 项目的补充说明，我们会在这里展示如何读取Solana数据，如何将数据存储到数据库中，并给出一些简单用途场景的查询方案。

Solana Events API: https://rapidapi.com/deepdig-deepdig-default/api/solana-events

## Set up Clickhouse
You can refer 'clickhouse/README.md' to set up Clickhouse instance, and create database table with following SQL

```
CREATE TABLE solana.token_swap_event
(
    `parseTime` UInt64,
    `slot` UInt64,
    `blockTime` UInt64,
    `blockHash` String,
    `signature` String,
    `programId` String,
    `instructionIndex` Float64,
    `swapSigner` String,
    `swapInUiAmount` Float64,
    `swapInTokenAddress` String,
    `swapOutUiAmount` Float64,
    `swapOutTokenAddress` String,
    `poolAddress` String,
    `poolBaseTokenAddress` String,
    `poolBaseTokenBalanceUiAmount` Float64,
    `poolQuoteTokenAddress` String,
    `poolQuoteTokenBalanceUiAmount` Float64,
    INDEX idx_blocktime blockTime TYPE minmax GRANULARITY 1
)
ENGINE = ReplacingMergeTree(parseTime)
PARTITION BY toStartOfDay(toDateTime(blockTime, 'UTC'))
ORDER BY (blockTime, signature, instructionIndex)
SETTINGS index_granularity = 8192
```

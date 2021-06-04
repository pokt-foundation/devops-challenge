# Pocket Foundation DevOps Challenge

## Problem
The Pocket Foundation runs multiple nodes of many different blockchains such as Ethereum, Binance Smart Chain, and xDAI. Some of these nodes run long-term without issues and are considered stable. Some of these nodes are not.

It is our responsibility to provide data from these blockchain nodes whether or not they are stable. To that end, we run multiple nodes of each type behind nginx. We require a monitoring and alerting system that will cover all of the blockchain server architecture.

## Deliverable
As a deliverable for this challenge, we would like to see how you would architect for this real-world problem by returning a Functional Specification Document or other method of illustrating your solutions. There are no specific requirements on the format of the deliverable.

## Requirements
### Monitoring of Blockchain nodes

Blockchain nodes often respond to multiple ways of checking health:

- Is this node healthy? (health check)
- Is this node fully synced? (sync check)
- What is the current block number? (block number check)
- Does this node have peers? (peer check)

The calls that you make to a node to check these health responses vary based on the node. Many nodes are based on Ethereum and will respond to the same checks as Ethereum, such as this block number check:

```
curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc": "2.0", "id": 1, "method": "eth_blockNumber", "params": []}' localhost:8545
```

Some nodes will not have a sync check and to make sure that the node is synced will require another method of comparison, such as to an outside oracle.


### Monitoring of Docker host health

The instances on which the nodes run should be monitored for basic health: CPU load, RAM, free space, etc.

### Dashboards

Dashboards for monitoring should encompass one overall dashboard showing the health of all nodes at once with optional drill down screens for each individual chain.

### Notifications

A SaaS notification system should be employed such as PagerDuty. Simultaneous alerting to a shared Discord channel is also an option but the notification system should be robust and allow for support rotations and multiple levels of alerts.

## Current Standards
- All nodes currently exist only in one AWS region, in multiple subnets. In the future, nodes may exist in multiple regions.
- EC2 instances running the blockchain nodes are tagged with tags indicating which blockchains exist on that instance; lists of nodes to monitored should be pulled dynamically via AWS tags.

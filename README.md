# Rewards Token Staking Ethereum Smart Contract

This repository contains the smart contract code for Reward ERC-20 Token & its simple Staking contract

`solc` version 0.8.0

## Setup Project

Install dependencies by

    `npm install`

## Run tests

 The project is built with `truffle`. To run all test cases, Please run

    `truffle test` 
    (or)
    `npm run test`

## Coverge report

 `solidity-coverage` does the coverage report. to run it,

    `npm run coverage` 
    (or)
    `truffle run coverage` 


Reference: [prestaking.sol](https://github.com/dusk-network/prestaking-contract/blob/master/contracts/Prestaking.sol).
Borrowed rewards calculation logic & staker struct & user clean up ideas from the above mentioned source, But modified to suit our use case.
```
    // Calculate percentage of reward to be received, and allocate it.
    // Reward is calculated down to a precision of two decimals.
    uint256 reward = staker.amount.mul(10000).mul(dailyReward).div(stakingPool).div(10000);
    staker.accumulatedReward = staker.accumulatedReward.add(reward);
```

## User journey
An account with some balance of the tokens can deposit them into the staking contract (which also has the tokens and distributes them over time). As the time goes by and blocks are being produced, this user should accumulate more of the tokens and can claim the rewards and withdraw the deposit.

## RewardToken.sol
This contract defines an ERC20 token that will be used for staking/rewards. The owner should be able to mint the token, change reward rates and enable/disable withdraw fees (also modifiable)

## Staker.sol
This contract will get deployed with some tokens minted for the distribution to the stakers. And then, according to a schedule, allocate the reward tokens to addresses that deposited those tokens into the contract. The schedule is up to you, but you could say that every block 100 tokens are being distributed; then you'd take the allocated tokens and divide by the total balance of the deposited tokens so each depositor get's proportional share of the rewards. Ultimately, a user will deposit some tokens and later will be able to withdraw the principal amount plus the earned rewards. The following functions must be implemented: deposit(), withdraw()

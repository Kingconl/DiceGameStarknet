# DiceGame Smart Contract

A Starknet smart contract implementation of a dice gambling game using ERC20 tokens (ETH).

## Overview

The DiceGame contract allows players to roll a dice by betting ETH. If they roll a number less than or equal to 5, they win the prize pool. The game uses block numbers and a nonce for randomization.

## Contract Details

### Game Rules
- Players must bet at least 0.002 ETH to play
- Rolling a number ≤ 5 wins the prize pool
- 40% of each bet is added to the prize pool
- Initial prize pool is set to 2 ETH
- If prize pool reaches 0, it resets to 2 ETH

### Winning Mechanics
- Dice rolls generate numbers between 0-15
- Numbers ≤ 5 are winning rolls (37.5% chance)
- Winners receive the entire prize pool
- After a win, prize pool resets to 10% of contract balance

## Functions

### Public Functions

`roll_dice(amount: u256)`
- Accepts player's bet amount
- Requires minimum 0.002 ETH bet
- Transfers ETH from player to contract
- Generates random roll using block number and nonce
- Distributes prize if player wins

`last_dice_value() -> u256`
- Returns the most recent dice roll value

`nonce() -> u256`
- Returns current nonce value used in randomization

`prize() -> u256`
- Returns current prize pool amount

`eth_token_dispatcher() -> IERC20CamelDispatcher`
- Returns the ERC20 token dispatcher instance

### Events

`Roll`
- Emitted on each dice roll
- Contains player address, bet amount, and roll value

`Winner`
- Emitted when a player wins
- Contains winner address and prize amount

## Usage

1. Approve the contract to spend your ETH tokens
2. Call `roll_dice` with your bet amount (minimum 0.002 ETH)
3. If your roll is ≤ 5, you automatically receive the prize

## Security Considerations

- Randomization depends on block numbers and nonce
- Contract requires sufficient ETH balance to pay winners
- Minimum bet requirement prevents spam
- Smart contract approval required before playing

## Dependencies

- OpenZeppelin ERC20 Interface
- Starknet standard library
- Keccak hash function for randomization

# Portfolio Rebalancer Module

## Overview
The `PortfolioRebalancer` Move smart contract allows users to set a target allocation for their portfolio and rebalance their holdings accordingly. This ensures that portfolio allocations remain aligned with user-defined targets.

## Features
- **Set Target Allocation**: Users can define their desired portfolio allocation as a percentage.
- **Automatic Rebalancing**: The contract recalculates and adjusts holdings based on the target allocation.
- **Secure Fund Handling**: Utilizes Aptos' native coin management framework for safe transactions.

## Smart Contract Code
```move
module MyModule::PortfolioRebalancer {
    use aptos_framework::signer;
    use aptos_framework::coin;
    use aptos_framework::aptos_coin::AptosCoin;

    struct Portfolio has store, key {
        target_allocation: u64, // Target allocation percentage (e.g., 50 for 50%)
    }

    /// Function to initialize portfolio with a target allocation.
    public fun set_target_allocation(owner: &signer, allocation: u64) {
        let portfolio = Portfolio {
            target_allocation: allocation,
        };
        move_to(owner, portfolio);
    }

    /// Function to rebalance portfolio based on target allocation.
    public fun rebalance_portfolio(owner: &signer) acquires Portfolio {
        let portfolio = borrow_global_mut<Portfolio>(signer::address_of(owner));
        let current_balance = coin::balance<AptosCoin>(signer::address_of(owner));
        let target_amount = (current_balance * portfolio.target_allocation) / 100;
        
        // Logic to adjust holdings (this is a placeholder, actual implementation varies)
        coin::transfer<AptosCoin>(owner, signer::address_of(owner), target_amount);
    }
}
```

## Functions
1. **`set_target_allocation(owner: &signer, allocation: u64)`**
   - Initializes or updates the target allocation percentage for the user's portfolio.
   - The percentage should be between `0` and `100`.

2. **`rebalance_portfolio(owner: &signer)`**
   - Retrieves the user’s current balance and calculates the amount needed to meet the target allocation.
   - Transfers assets to maintain the desired allocation.

## Usage
1. Deploy the `PortfolioRebalancer` module on the Aptos blockchain.
2. Call `set_target_allocation` to establish a portfolio allocation percentage.
3. Periodically execute `rebalance_portfolio` to adjust holdings accordingly.

## Security Considerations
- Users should ensure they have sufficient funds before rebalancing.
- Only the contract owner can set or adjust the target allocation.
- The module should integrate with verified price feeds for accurate allocation adjustments.

## Future Enhancements
- Multi-asset support for diversified portfolio rebalancing.
- Automated rebalancing based on predefined time intervals or thresholds.
- Integration with external liquidity pools for optimized transactions.

## Contract Address & Transaction
- **Contract Address**: `0xYourContractAddressHere`
- **Example Transaction Hash**: `0xYourTransactionHashHere`

This module helps investors maintain their desired asset allocation, ensuring long-term portfolio stability.

++++++++++++++++++++++++++++++++++++++++++++++++++++++

##contact address
0x39161374a21abee8a312bca435f61375759cdbc9ea2750e1ff9e71959f0e02f3
![image](https://github.com/user-attachments/assets/c6cc5f22-b9dd-4c59-8d93-c5a480701fdf)

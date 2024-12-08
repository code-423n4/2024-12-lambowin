# Lambo.win audit details
- Total Prize Pool: $22,500 in USDC
  - HM awards: $17,952 in USDC
  - QA awards: $748 in USDC
  - Judge awards: $2,000 in USDC
  - Scout awards: $500 in USDC
  - Validator awards: $1,300 in USDC
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts December 2, 2024 20:00 UTC
- Ends December 9, 2024 20:00 UTC

**Note re: risk level upgrades/downgrades**

Two important notes about judging phase risk adjustments: 
- High- or Medium-risk submissions downgraded to Low-risk (QA)) will be ineligible for awards.
- Upgrading a Low-risk finding from a QA report to a Medium- or High-risk finding is not supported.

As such, wardens are encouraged to select the appropriate risk level carefully during the submission phase.

## Automated Findings / Publicly Known Issues

The 4naly3er report can be found [here](https://github.com/code-423n4/2024-11-lambowin/blob/main/4naly3er-report.md).

_Note for C4 wardens: Anything included in this `Automated Findings / Publicly Known Issues` section is considered a publicly known issue and is ineligible for awards._

1. Rebalance Contract ignore gas cost
The RebalanceOnUniswap contract is designed to maintain the VETH/WETH pool ratio at 1:1 rather than for profit. Gas costs are intentionally omitted to increase rebalancing frequency, accepting gas losses as a trade-off for improved price stability.

2. repayLoan function not used
The repayLoan function in the VirtualToken contract is currently not used. This function is designed to allow valid factories to repay loans by decreasing the debt of a user and 1. burning the corresponding amount of tokens.

We hope to provide services for subsequent liquidity additions. If the withdrawable feature of virtual liquidity can be realized, it will be able to solve the impermanent loss problem of Uniswap V2. We plan to release LamboFactory V2 and conduct audit again.


# Overview

## LamboV2: An Efficient, Near-Zero Cost Liquidity Solution for Token Launch

In the realm of cryptocurrency, liquidity is paramount, especially for nascent Meme projects. Liquidity refers to the ease with which assets can be bought or sold in the market without affecting their price. For cryptocurrency projects, having sufficient liquidity is crucial for several reasons.

To search for an efficient, near-zero cost liquidity solution for token launch, we propose a straightforward mechanism: the concept of virtual liquidity to meet the liquidity needs of project parties. We will establish a deep liquidity pool on UniswapV3 to satisfy the liquidity exit for users' buying and selling activities. Essentially, this mechanism involves whales providing liquidity to retail investors. Liquidity providers can earn profits through LP fees, creating a win-win situation where whales earn LP fees and retail investors/developers resolve their liquidity issues.

We believe this mechanism can enhance the liquidity returns for DeFi whales while simultaneously addressing the liquidity challenges faced by retail investors and developers.

## Virtual Liquidity
Virtual liquidity is a conditional ERC20 token. For each holder address of virtual liquidity, the transferable balance must satisfy the following formula to ensure that the issued virtual liquidity does not enter the market.

```
transferable_balance = balance - debt
```
where Debt is always less than or equal to the balance.

## Framework

This is the core contract of Lambo.win:
1. VirtualToken
2. LamboFactor
3. LamboRouter

![img](https://github.com/code-423n4/2024-11-lambowin/blob/main/framework.png?raw=true)

## Peg And Repeg

We will deploy liquidity on Uniswap V3, and the `LamboRebalanceOnUniwap` contract is responsible for rebalancing the Uniswap V3 pool. The Rebalance contract utilizes the flash loan mechanism to perform arbitrage operations through MorphoVault. Specifically, the Rebalance contract executes buy or sell operations in the Uniswap V3 pool to ensure the pool's balance and gain profit through arbitrage.
![Defintion](https://github.com/code-423n4/2024-11-lambowin/blob/main/Lambo-VirtualToken.png?raw=true)

In Uniswap V3, Lambo's LP needs to have two ranges:
1. Peg Zone
2. Repeg Zone

The Peg Zone is designed to allow low slippage exchanges between vETH and ETH. The purpose of the Repeg Zone is to create slippage, allowing the Rebalance contract to trigger timely rebalancing with profit margins to subsidize LP fees, thereby enabling cost-free flash loans.


## Links

- **Previous audits:**  [audit/SlowMistAudit.pdf](https://github.com/code-423n4/2024-11-lambowin/blob/main/audit/SlowMistAudit.pdf)
- **Documentation:** [doc/LamboV2.pdf](https://github.com/code-423n4/2024-11-lambowin/blob/main/doc/LamboV2.pdf)
- **Website:** [lambo.win/launchpool](https://lambo.win/launchpool)
- **X/Twitter:** https://x.com/lambodotwin

---

# Scope

*See [scope.txt](https://github.com/code-423n4/2024-11-lambowin/blob/main/scope.txt)*

### Files in scope


| File   | Logic Contracts | Interfaces | nSLOC | Purpose | Libraries used |
| ------ | --------------- | ---------- | ----- | -----   | ------------ |
| /src/LamboFactory.sol | 1| **** | 58 | |@openzeppelin/contracts/proxy/Clones.sol<br>@openzeppelin/contracts/token/ERC20/IERC20.sol<br>@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol<br>@openzeppelin/contracts/access/Ownable.sol<br>@openzeppelin/contracts/utils/ReentrancyGuard.sol|
| /src/LamboToken.sol | 1| **** | 122 | |@openzeppelin/contracts/token/ERC20/IERC20.sol<br>@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol<br>@openzeppelin/contracts/utils/Context.sol<br>@openzeppelin/contracts/interfaces/draft-IERC6093.sol<br>@openzeppelin/contracts/access/Ownable.sol|
| /src/LamboVEthRouter.sol | 1| **** | 115 | |@openzeppelin/contracts/token/ERC20/IERC20.sol<br>@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol<br>@openzeppelin/contracts/access/Ownable.sol<br>@openzeppelin/contracts/utils/ReentrancyGuard.sol|
| /src/VirtualToken.sol | 1| **** | 117 | |@openzeppelin/contracts/token/ERC20/ERC20.sol<br>@openzeppelin/contracts/token/ERC20/IERC20.sol<br>@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol<br>@openzeppelin/contracts/access/Ownable.sol|
| /src/rebalance/LamboRebalanceOnUniwap.sol | 1| **** | 131 | |@openzeppelin/contracts-upgradeable/proxy/utils/UUPSUpgradeable.sol<br>@openzeppelin/contracts-upgradeable/access/OwnableUpgradeable.sol<br>@openzeppelin/contracts/token/ERC20/IERC20.sol<br>@openzeppelin/contracts-upgradeable/proxy/utils/Initializable.sol<br>@openzeppelin/contracts-upgradeable/utils/ReentrancyGuardUpgradeable.sol<br>@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol<br>@morpho/interfaces/IMorpho.sol<br>@morpho/interfaces/IMorphoCallbacks.sol|
| /src/Utils/LaunchPadUtils.sol | 1| **** | 10 | ||
| src/libraries/UniswapV2Library.sol | - | **** | 48 | ||
| **Totals** | **6** | **** | **601** | | |

### Files out of scope

*See [out_of_scope.txt](https://github.com/code-423n4/2024-11-lambowin/blob/main/out_of_scope.txt)*

## Scoping Q &amp; A




| Question                                | Answer                       |
| --------------------------------------- | ---------------------------- |
| ERC20 used by the protocol              |    USDC, USDT            |
| Test coverage                           | 55.10% (243/441 of statements)                         |
| ERC721 used  by the protocol            |            None              |
| ERC777 used by the protocol             |           None                |
| ERC1155 used by the protocol            |              None            |
| Chains the protocol will be deployed on | Ethereum |

### External integrations (e.g., Uniswap) behavior in scope:


| Question                                                  | Answer |
| --------------------------------------------------------- | ------ |
| Enabling/disabling fees (e.g. Blur disables/enables fees) | Yes   |
| Pausability (e.g. Uniswap pool gets paused)               |  No   |
| Upgradeability (e.g. Uniswap gets upgraded)               |   No  |


### EIP compliance checklist
N/A


# Additional context

## Main invariants

N/A

## Attack ideas (where to focus for bugs)
1.  The V3 Liquidity (VETH <-> WETH)'s safety
2. The ETH locked in VETH's safety
3. The complicated scenario with unsiwapV2, V3 and VETH's take loan 


## All trusted roles in the protocol

The owner of vETH, LamboRouter, LamboFactory and the RebalanceContract is trusted

## Describe any novel or unique curve logic or mathematical models implemented in the contracts:

Virtual liquidity is a conditional ERC20 token. For each holder address of virtual liquidity, the transferable balance must satisfy the following formula to ensure that the issued virtual liquidity does not enter the market.


## Running tests

```bash
git clone https://github.com/code-423n4/2024-12-lambowin.git
cd 2024-12-lambowin
forge build
forge test
```

| File                                     | % Lines          | % Statements     | % Branches      | % Funcs         |
|------------------------------------------|------------------|------------------|-----------------|-----------------|
| src/LamboFactory.sol                     | 50.00% (17/34)   | 50.00% (17/34)   | 0.00% (0/8)     | 50.00% (6/12)   |
| src/LamboToken.sol                       | 38.68% (41/106)  | 39.29% (44/112)  | 13.33% (4/30)   | 38.24% (13/34)  |
| src/LamboVEthRouter.sol                  | 44.00% (44/100)  | 44.44% (56/126)  | 2.38% (1/42)    | 44.44% (8/18)   |
| src/VirtualToken.sol                     | 53.33% (48/90)   | 58.00% (58/100)  | 9.62% (5/52)    | 52.94% (18/34)  |
| src/rebalance/LamboRebalanceOnUniwap.sol | 98.25% (56/57)   | 98.55% (68/69)   | 34.62% (9/26)   | 90.91% (10/11)  |
| Total                                    | 53.23% (206/387) | 55.10% (243/441) | 12.03% (19/158) | 50.46% (55/109) |

## Miscellaneous
Employees of Lambo.win and employees' family members are ineligible to participate in this audit.

Code4rena's rules cannot be overridden by the contents of this README. In case of doubt, please check with C4 staff.




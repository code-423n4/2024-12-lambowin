# ✨ So you want to run an audit

This `README.md` contains a set of checklists for our audit collaboration.

Your audit will use two repos: 
- **an _audit_ repo** (this one), which is used for scoping your audit and for providing information to wardens
- **a _findings_ repo**, where issues are submitted (shared with you after the audit) 

Ultimately, when we launch the audit, this repo will be made public and will contain the smart contracts to be reviewed and all the information needed for audit participants. The findings repo will be made public after the audit report is published and your team has mitigated the identified issues.

Some of the checklists in this doc are for **C4 (🐺)** and some of them are for **you as the audit sponsor (⭐️)**.

---

# Audit setup

## 🐺 C4: Set up repos
- [ ] Create a new private repo named `YYYY-MM-sponsorname` using this repo as a template.
- [ ] Rename this repo to reflect audit date (if applicable)
- [ ] Rename audit H1 below
- [ ] Update pot sizes
  - [ ] Remove the "Bot race findings opt out" section if there's no bot race.
- [ ] Fill in start and end times in audit bullets below
- [ ] Add link to submission form in audit details below
- [ ] Add the information from the scoping form to the "Scoping Details" section at the bottom of this readme.
- [ ] Add matching info to the Code4rena site
- [ ] Add sponsor to this private repo with 'maintain' level access.
- [ ] Send the sponsor contact the url for this repo to follow the instructions below and add contracts here. 
- [ ] Delete this checklist.

# Repo setup

## ⭐️ Sponsor: Add code to this repo

- [ ] Create a PR to this repo with the below changes:
- [ ] Confirm that this repo is a self-contained repository with working commands that will build (at least) all in-scope contracts, and commands that will run tests producing gas reports for the relevant contracts.
- [ ] Please have final versions of contracts and documentation added/updated in this repo **no less than 48 business hours prior to audit start time.**
- [ ] Be prepared for a 🚨code freeze🚨 for the duration of the audit — important because it establishes a level playing field. We want to ensure everyone's looking at the same code, no matter when they look during the audit. (Note: this includes your own repo, since a PR can leak alpha to our wardens!)

## ⭐️ Sponsor: Repo checklist

- [ ] Modify the [Overview](#overview) section of this `README.md` file. Describe how your code is supposed to work with links to any relevent documentation and any other criteria/details that the auditors should keep in mind when reviewing. (Here are two well-constructed examples: [Ajna Protocol](https://github.com/code-423n4/2023-05-ajna) and [Maia DAO Ecosystem](https://github.com/code-423n4/2023-05-maia))
- [ ] Review the Gas award pool amount, if applicable. This can be adjusted up or down, based on your preference - just flag it for Code4rena staff so we can update the pool totals across all comms channels.
- [ ] Optional: pre-record a high-level overview of your protocol (not just specific smart contract functions). This saves wardens a lot of time wading through documentation.
- [ ] [This checklist in Notion](https://code4rena.notion.site/Key-info-for-Code4rena-sponsors-f60764c4c4574bbf8e7a6dbd72cc49b4#0cafa01e6201462e9f78677a39e09746) provides some best practices for Code4rena audit repos.

## ⭐️ Sponsor: Final touches
- [ ] Review and confirm the pull request created by the Scout (technical reviewer) who was assigned to your contest. *Note: any files not listed as "in scope" will be considered out of scope for the purposes of judging, even if the file will be part of the deployed contracts.*
- [ ] Check that images and other files used in this README have been uploaded to the repo as a file and then linked in the README using absolute path (e.g. `https://github.com/code-423n4/yourrepo-url/filepath.png`)
- [ ] Ensure that *all* links and image/file paths in this README use absolute paths, not relative paths
- [ ] Check that all README information is in markdown format (HTML does not render on Code4rena.com)
- [ ] Delete this checklist and all text above the line below when you're ready.

---

# Lambo.win audit details
- Total Prize Pool: $22500 in USDC
  - HM awards: $17952 in USDC
  - (remove this line if there is no Analysis pool) Analysis awards: XXX XXX USDC (Notion: Analysis pool)
  - QA awards: $748 in USDC
  - (remove this line if there is no Bot race) Bot Race awards: XXX XXX USDC (Notion: Bot Race pool)
 
  - Judge awards: $2000 in USDC
  - Validator awards: XXX XXX USDC (Notion: Triage fee - final)
  - Scout awards: $500 in USDC
  - (this line can be removed if there is no mitigation) Mitigation Review: XXX XXX USDC (*Opportunity goes to top 3 backstage wardens based on placement in this audit who RSVP.*)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts November 27, 2024 20:00 UTC
- Ends December 4, 2024 20:00 UTC

**Note re: risk level upgrades/downgrades**

Two important notes about judging phase risk adjustments: 
- High- or Medium-risk submissions downgraded to Low-risk (QA)) will be ineligible for awards.
- Upgrading a Low-risk finding from a QA report to a Medium- or High-risk finding is not supported.

As such, wardens are encouraged to select the appropriate risk level carefully during the submission phase.

## Automated Findings / Publicly Known Issues

The 4naly3er report can be found [here](https://github.com/code-423n4/2024-11-lambowin/blob/main/4naly3er-report.md).



_Note for C4 wardens: Anything included in this `Automated Findings / Publicly Known Issues` section is considered a publicly known issue and is ineligible for awards._
## 🐺 C4: Begin Gist paste here (and delete this line)





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
| **Totals** | **6** | **** | **553** | | |

### Files out of scope

*See [out_of_scope.txt](https://github.com/code-423n4/2024-11-lambowin/blob/main/out_of_scope.txt)*

| File         |
| ------------ |
| ./script/0.deployTokens.s.sol |
| ./script/1.deployOthers.s.sol |
| ./script/2.ownerTransfer.s.sol |
| ./script/3.deployRebalacne.s.sol |
| ./script/quoter/DeployQuoter.s.sol |
| ./script/quoter/LamboMemeQuoter.sol |
| ./script/quoter/LamboQuoterForAggregator.sol |
| ./script/quoter/LamboQuoterPathFor1inchV6.sol |
| ./src/interfaces/1inchV6/IAggregator.sol |
| ./src/interfaces/Curve/IStableNGFactory.sol |
| ./src/interfaces/Curve/IStableNGPool.sol |
| ./src/interfaces/IApprove.sol |
| ./src/interfaces/IApproveProxy.sol |
| ./src/interfaces/IFactory.sol |
| ./src/interfaces/ILaunchpad.sol |
| ./src/interfaces/IPool.sol |
| ./src/interfaces/IPoolFactory.sol |
| ./src/interfaces/IPoolRegistery.sol |
| ./src/interfaces/IRouter.sol |
| ./src/interfaces/IWETH.sol |
| ./src/interfaces/OKX/IDexRouter.sol |
| ./src/interfaces/Uniswap/ILiquidityManager.sol |
| ./src/interfaces/Uniswap/INonfungiblePositionManager.sol |
| ./src/interfaces/Uniswap/IPool.sol |
| ./src/interfaces/Uniswap/IPoolFactory.sol |
| ./src/interfaces/Uniswap/IPoolInitializer.sol |
| ./src/interfaces/Uniswap/IQuoter.sol |
| ./src/interfaces/Uniswap/IUniswapV2Router01.sol |
| ./src/interfaces/Uniswap/IUniswapV3Pool.sol |
| ./src/libraries/1inchV6.sol |
| ./src/libraries/AddressLib.sol |
| ./src/libraries/ProtocolLib.sol |
| ./src/libraries/UniswapV2Library.sol |
| ./test/BaseTest.t.sol |
| ./test/GeneralTest.t.sol |
| ./test/LiquidityManage.t.sol |
| ./test/RebalanceTest.t.sol |
| ./test/tools/TestLamboMemeQuoter.t.sol |
| ./test/tools/TestLamboQuoterForAggregator.t.sol |
| Totals: 39 |

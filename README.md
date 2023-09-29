# Corego

> This document will be part of the terms and conditions of your agreement and therefore needs to contain all the required information about the project. Don't remove any of the mandatory parts presented in bold letters or as headlines (except for the title)! Lines starting with a `>` (such as this one) should be removed. Please use markdown instead of HTML (e.g. `![](image.png)` instead of `<img>`).
> 
> See the [Grants Program Process](https://github.com/w3f/Grants-Program/#pencil-process) on how to submit a proposal.

- **Team Name:** Legal name of your team (e.g. JsonCorp)
- **Payment Address:** In the case of fiat payment, please share your bank account privately with grants@web3.foundation via your contact email (see below) and enter the date when you shared the information with us (e.g. Fiat 24.12.1971, 11:59) here. Otherwise, provide the Polkadot (for USDC & USDT) or Bitcoin payment address. Please also specify the currency. (e.g. 0x8920... (USDC))
- **[Level](https://github.com/w3f/Grants-Program/tree/master#level_slider-levels):** 1, 2 or 3

> ❗ *The combination of your GitHub account submitting the application and the payment address above will be your unique identifier during the program. Please keep them safe.*

## Project Overview 📄

### Overview

- Corego is a marketplace and a set of tools for Coretime manipulation and data tracking, with the goal of making development on Polkadot faster, easier, more flexible, and as an end result cheaper.
- Corego is a project that builds upon the ideas presented in the Agile Coretime RFC. The project will be developed under the assumption that the functionality described in the RFC will be implemented within the Polkadot/Kusama ecosystem.
  Given that the pallet containing all the logic presented in the RFC already exists, we will have the capability to undertake all the development outlined in this proposal.
* Creating proper tooling and a market for Coretime can have a significant impact on the development that takes place on Polkadot. It will enable experiments and small personal projects to be deployed to Polkadot with minimal effort and cost.

### Project Details

The project essentially consists of four parts that will create a cohesive application. In the following sections, each of them is described in great detail.

#### Coretime Abstractions

Considering that the entire project is built upon the ideas presented in the Agile Coretime RFC, there is a clear requirement to allow users to perform actions on their Coretime using Corego.


- **Regions Dashboard** will serve as a central hub for users, allowing them to browse all of the regions they own. The regions will be presented as UI card components containing all relevant metadata and actions that a user can perform on their region.
  TODO: IMAGE

- **Partitioning** UI will offer users a convenient method for splitting their region. The UI will visually represent the region as a timeline, highlighting all potential pivotal points available for partitioning.

  <p align="center">
    <img width="800" src="https://i.postimg.cc/zB7y0tkk/parititoning-v2.png"/>
  </p>

- **Interlacing** UI will also allow users to easily interlace the region they own. The user will be able to specify the region core mask as a fraction. The UI will visually show a block colored with a distinct color based on the fraction. TODO: Provide a better image
  <p align="center">
    <img width="400" src="https://i.postimg.cc/brdwLzrz/image.png"/>
  </p>

- **Naming Regions & Tasks**: Users will have the option to assign names to their regions and tasks, making it simple to differentiate them.

- **Assignment** UI will make it straightforward for users to allocate a task to their owned regions. The UI will display a dropdown menu containing all the tasks that the user has published to the relay chain, simplifying the selection process. TODO: better image
  <p align="center">
    <img width="500" src="https://i.postimg.cc/ncjLDcN2/image-2.png"/>
  </p>

- **Transfer** UI will offer a straightforward modal for users to perform transfers. TODO: better image
  <p align="center">
    <img width="400" src="https://i.postimg.cc/k59MzNGY/transfer.png"/>
  </p>

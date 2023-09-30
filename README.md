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
    <img width="300" src="https://i.postimg.cc/brdwLzrz/image.png"/>
  </p>

- **Naming Regions & Tasks**: Users will have the option to assign names to their regions and tasks, making it simple to differentiate them.

- **Assignment** UI will make it straightforward for users to allocate a task to their owned regions. The UI will display a dropdown menu containing all the tasks that the user has published to the relay chain, simplifying the selection process. TODO: better image
  <p align="center">
    <img width="400" src="https://i.postimg.cc/ncjLDcN2/image-2.png"/>
  </p>

- **Transfer** UI will offer a straightforward modal for users to perform transfers. TODO: better image
  <p align="center">
    <img width="300" src="https://i.postimg.cc/k59MzNGY/transfer.png"/>
  </p>

#### Secondary Market

Coretime is a resource that goes to waste if not utilized during its intended time. When you purchase a core for a month, it means you can use a maximum of one core at any given moment during that specific time period. If the core is not utilized, the coretime is essentially squandered.

After buying coretime during the bulk period, one may realize that the purchased coretime is either too much or too little for the intended use. The secondary market assists these individuals and teams in rectifying their mistakes by enabling them to potentially sell or buy more coretime.

Coretime can be partitioned and interlaced meaning most of the coretime on sale will hardly be the same. For this reason we are going to utilise the order book model.

The seller will need to specify the price for the entire region, and based on that, the contract will calculate the price of one bit, which is equivalent to 1/80th of the price of the entire region.

This means that the total value of the coretime owned by the seller will go down every time the smallest unit of computation is not used. From here, we can come to the conclusion that the price of the region that is being on sale is dynamic.

**The steps of selling and buying coretime:**

1.  A user decides to sell one of their regions.
	-   The user defines the price that they intend to sell the region for.
	-   The contract calculates the price per one bit. 
2.  Another user decides to buy some coretime.
	-   They are browsing the market, and they have decided they want to buy a specific region.   
	-   The user will have to pay the price for the region; however, this won't be the price of the entire region. The price will be defined by remaining_smallest_units * price_per_unit.
3.  The user pays the price, the seller receives the paid amount, and the buyer receives the region.

In case a user doesn't want to buy the entire region but only a part of it, the buyer will need to specify which parts of the region they want and provide the steps to actually create a region that has the properties they desire.
The contract will be able to follow the steps the buyer provides and create a region that the buyer wants to buy. The contract will also calculate the amount that needs to be paid for that and charge the buyer the appropriate amount. After all these steps, the seller will receive their tokens, and the buyer will obtain their desired coretime.
We refer to this feature  **Region Derivation**. It will enable buyers to have more options when purchasing coretime, making it easier to meet their specific needs.

TODO: Should we provide an example here from the market doc?

**Defining the price of coretime**
The price of coretime will be highly influenced by supply and demand. Since we are constructing a market with an NFT order book model, users will have the authority to establish the price of the coretime they intend to sell.

Depending on whether the seller owns an entire core, only partitioned parts, or has it interlaced, the selling price of the coretime will be affected.

As mentioned earlier, the pricing of a region will be determined at a bit level. This approach proves particularly useful because it allows us to establish a pricing structure that decreases when coretime is wasted.

In situations where the buyer's instructions involve partitioning the region and performing interlacing on the partitioned region, the price will be determined based on the bit price of the resulting partitioned region.

This approach allows us to easily calculate the price of the region the buyer intends to purchase, even in situations where the buyer requires multiple instructions to be executed on the region.

**Formula to calculate the price when partitioning:**
`price = bit_price * pivot_defined_as_bit`

**Formula to calculate the price when interlacing:**
`price = bit_price * new_region_length_in_bits`

TODO: Should we provide an example here from the market doc?

**Region Derivation**
As demonstrated in the previous example, buyers have the option to acquire only a portion of a region. This is achieved by requesting a set of instructions from the buyer to generate the desired region. However, manually specifying these instructions can be a challenging task for users.

The approach we aim to adopt here is to enable users to describe the desired characteristics of the region they require. Using all the provided input, the frontend will determine whether the specified region can be generated from all regions listed on the market. If a match is found, the user will be presented with a price for their region. Future iterations of this feature may include Natural Language Processing (NLP) to describe the region’s characteristics.

**Market Architecture**
The coretime marketplace can be implemented in four different ways, which include:

1.  Ink! smart contract
2.  Solidity smart contract
3.  Actor (Not yet implemented in Polkadot/Kusama)
4.  Parachain

From these options, we've selected the Ink! smart contract as our initial approach. As the project evolves, we anticipate transitioning to either an actor or a separate parachain to access greater possibilities to improve our services.
We possess a much more comprehensive overview of all these options, which we chose not to include here to avoid making this proposal too lengthy. However, we can provide it if there is interest.

**Implementation Requirements**
We came up with an implementation design that makes it possible to develop the market as an ink! smart contract located on a contracts parachain in the Polkadot/Kusama ecosystem.
Our solution has very minimal and reasonable assumptions that are required to make this possible. 

Our sole assumption is that the concepts outlined in the Agile Coretime RFC are implemented in Polkadot/Kusama. We do not have any specific assumptions concerning the XCM configuration on the Coretime parachain to make this work. We only require that the Coretime parachain allows basic reserve transfers.

The only feature with a slightly greater assumption is region derivation. To enable region derivation, we need the Coretime parachain to support the `Transact` XCM instruction. 
This is because regions can only be partitioned or interlaced on the Coretime parachain. Consequently, during region derivation, the region must be transferred to the Coretime parachain, where all instructions are executed (this is where the `Transact` instruction is required). Subsequently, the new regions are transferred back to the contracts parachain, where one of the regions is sent to the buyer, while the remaining regions are listed again on the market.

**Region NFT Contract**
To create a marketplace on a contracts parachain, we'll need an NFT region contract. We'll use the openbrush library to simplify development, as it will only require a few adjustments.

TODO: Should I add the in-depth details how cross-chain region transfers will work?

#### Data Dashboard

Corego's Data Dashboard is a central hub for users, offering essential insights and real-time market data. With a user-friendly interface, it provides context, data from the Coretime chain, market information, and other useful insights. This empowers users to make informed decisions, whether they are buying or selling coretime or performing other operations.

We have divided the data dashboard into four sections.

**1. Constants**
Displaying configuration constants to the user is be highly beneficial, giving them a more comprehensive macro understanding of the system.

For instance, by tracking the volume of coretime channeled into the Instantaneous Coretime Pool, we can gauge the prevailing demand for coretime. Delving deeper, we could measure pool payouts and determine a ratio comparing the volume of coretime sold in the pool to the volume deposited. Such metrics, among others, would provide invaluable information.

Data shown in the constants section:
-   Interlude Period Length: Time during which the bulk sale is not active.   
-   Leadin Period Length: Time during which the sale price varies.
-   Region length: The length of the regions available for purchase during the upcoming bulk sale.
-   Cores Limit: The maximum number of cores that can be sold.
-   Renewal Price Increase: The maximum price increase of a renewable region.

**2. Coretime Chain**
While we don't directly oversee the operations of the coretime chain, indexing data from the primary market can offer significant insights.

Data
-   Reserved Cores: Cores utilized by system parachains.
-   Renewed Cores: Cores renewed by non-system parachains.
-   Leases: Number of leases.
-   Current Bulk Sale Period: Ongoing period of bulk sale.
-   Bulk Sale Offerings: Number of cores offered in the bulk sale.
-   Bulk Sale Transactions: Number of cores sold.
-   Unassigned Regions: Total number of regions without assignments.
-   Assigned Regions: Total number of regions with assignments.
-   Region Status: Number of finalized and provisional regions.
-   Leadin Period Price Trend: Continuous decrease in bulk coretime price.
-   Post-Leadin Coretime Price: Price after the leadin period.
-   Core Utilization: Percentage of utilized cores (with a graph for time-based visualization).
-   Region Utilization: Percentage of utilized regions (with a graph for time-based visualization).
-   Instantaneous Pool Data
-   Contributor Input: Circle graph showcasing contributor-provided and system-provided bits, akin to the income graph on the dotreasury website.
-   Coretime Purchases: Volume purchased during a specific time frame.
-   Pending Payouts: Unclaimed payouts, reminiscent of the 'to be awarded' data on the dotreasury website. TODO: should we mention dotreasury?

**3. Market**
As the secondary market expands with increasing user transitions, it becomes crucial to index pertinent data.

For instance, by tracking daily, weekly, or other periodic purchases and sales, users can gain a clearer understanding of coretime's price trends. Moreover, real-time indexing of coretime's price can offer immediate insights. Such data indexing could pave the way for aggregators to present users with diverse liquidity options across multiple coretime markets akin to the 1inch protocol. TODO: Should we mention 1inch?

Data
-   Regions on sale (for a specified period)
-   Monthly Regions Sold (with future potentials for a ratio - (sold/on sale)).
-   Purchases: Number for a specified period (day, week, etc.).
-   Market Dominance: Share of secondary market.
-   Trading Volume: For a specified period in USD and DOT.
-   Total Transactions: Made between unique active wallets and contracts.
-   Total Users: Registered users with at least one market transaction.
-   Monthly Active Users: Registered users with at least one monthly transaction.
-   Average Price Per Timeslice: With a graph depicting data over time in USD and DOT.
-   Regions flowing in and out of the parachain where Corego is deployed.

**4. Tooling**

As outlined earlier, users have an array of tools at their disposal to modify their regions. Compiling data on these modifications, such as the number of interlaced or partitioned regions at any given moment, can offer robust insights into market activity and specialization.

Data:
*The number of occurrences during a specified time period:*
1.  Partitioning
2.  Interlacing
3.  Assignments
4.  Transfers

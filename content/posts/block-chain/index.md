---
title: "Block Chain"
description: What is Blockchain? Have you ever wondered want happens in decentralized transactions, where money sent can beseen publicly and records can not be erased. Join me here as I elaborate.
date: 2024-04-29
draft: false # this section allows the post to be published and be public, is it is set to true the post will not be published.
summary: "Web 3.0" # Here you can write a small summary of the post if needed
tags: [Web3.0 Intro]
categories: [Block Chain, Programming]
---

# BLOCKCHAIN BASICS


# **What is a Blockchain?**

### Bitcoin and Blockchain

You might be familiar with

```
Bitcoin
```

,
 which is one of the first protocols to utilize the revolutionary 
blockchain technology. The Bitcoin Whitepaper, authored by the 
pseudonymous

```
Satoshi Nakamoto
```

, described how Bitcoin could 
facilitate peer-to-peer transactions within a decentralized network 
using cryptography. This gave rise to censorship-resistant finance and 
presented

```
Bitcoin
```

as a superior digital store of value, often referred to as

*digital gold*

. There is a fixed amount of Bitcoin, similar to the scarcity of gold. You can learn more about this in the

[Bitcoin Whitepaper](https://bitcoin.org/bitcoin.pdf)

.

### Ethereum and Smart Contracts

A few years after Bitcoin's creation, Vitalik Buterin and others founded

```
Ethereum
```

,
 which builds upon the blockchain infrastructure, but with additional 
capabilities. With Ethereum, you can create decentralized transactions, 
organizations, and agreements without a centralized intermediary. This 
was achieved through the addition of

```
smart contracts
```

.

Though the concept of smart contracts was originally conceived in 1994 by

[**Nick Szabo**](https://en.wikipedia.org/wiki/Nick_Szabo)

, Ethereum made it a reality.

> Smart
 contracts are a set of instructions executed in a decentralized way 
without the need for a centralized or third party intermediary.
> 

Smart Contract functionality is the primary difference between blockchains like

```
Ethereum
```

and

```
Bitcoin
```

. Technically

```
Bitcoin
```

does have smart contracts but they're intentionally

```
turing incomplete
```

.

### The Oracle Problem

However,
 smart contracts face a significant limitation – they cannot interact 
with or access data from the real world. This is known as the

```
Oracle Problem
```

.

Blockchains
 are deterministic systems, so everything happens within their 
ecosystem. To make smart contracts more useful and capable of handling 
real-world data, they need external data and computation.

Oracles 
serve this purpose. They are devices or services that provide data to 
blockchains or run external computation. To maintain decentralization, 
it's necessary to use a decentralized Oracle network rather than relying
 on a single source. This combination of on-chain logic with off-chain 
data leads to

```
hybrid smart contracts
```

.

> Note:
> 

### Chainlink

[**Chainlink**](https://chain.link/)

is a popular decentralized Oracle network that enables smart contracts 
to access external data and computation. Chainlink is also blockchain 
agnostic - so it's going to work with any chain out there.

### Layer 2 Scaling Solutions

As
 blockchains grow, they face scaling issues. Layer 2, or L2, solutions 
have been developed to address this. L2 solutions involve other 
blockchains hooking into the main blockchain, essentially allowing it to
 scale. There are two primary types of L2 solutions:

- **Optimistic Rollups:** eg. Optimism, Arbitrum
- **Zero-Knowledge Rollups:** eg. ZK Sync, Polygon ZK EVM

Don't
 worry too much about this now. Once we understand how blockchains work 
'under the hood', we'll go further into Layer 2's then.

### Terminology

You're
 going to hear some terms used in this course (and the community as a 
whole) a little interchangeably. Maybe you haven't heard these terms 
before. I hope this offers a bit of clarification.

- Common Terms
    1. **Blockchain**: In web3, a blockchain is a digital
    ledger that records transactions across many computers in a secure and
    decentralized manner. Each block contains a number of transactions, and
    every new block is linked to the previous one, forming a chain. This
    makes the data tamper-resistant. *Example*: Bitcoin's blockchain records all BTC transactions.
    2. **Oracle**: Oracles in web3 are intermediaries that provide smart contracts with
    external data. They act as bridges between blockchains and the outside
    world, allowing smart contracts to execute based on real-world events
    and data. *Example*: A weather oracle provides data for a smart contract that triggers crop insurance payments based on rainfall data.
    3. **Layer 2**: Layer 2 solutions in web3 are technologies built on top of a blockchain (Layer 1) to improve its scalability and efficiency. These solutions
    handle transactions off the main chain, reducing congestion and fees,
    and then settle the final state on the main chain. *Example*: The Lightning Network for Bitcoin.
    4. **Dapp (Decentralized Application)**: A Dapp is an application that runs on a decentralized network,
    typically a blockchain. It is powered by smart contracts and operates
    without a central authority. Dapps can serve various purposes, from
    finance to gaming. *Example*: Uniswap, a decentralized finance application.
    5. **Smart Contract**: In web3, a smart contract is a self-executing contract with the terms
    of the agreement directly written into code. They run on blockchains and automatically execute when predetermined conditions are met, without
    the need for intermediaries. *Example*: A smart contract for an escrow service.
    6. **Hybrid Smart Contract**: Hybrid smart contracts combine on-chain code (running on a blockchain)
    with off-chain data and computations provided by oracles. This allows
    the contracts to interact with data and systems outside their native
    blockchain. *Example*: A smart contract for insurance that uses real-world data (like weather or flight delays) provided by oracles.
    7. **Ethereum/EVM (Ethereum Virtual Machine)**: Ethereum is a blockchain platform known for its smart contract
    functionality. The Ethereum Virtual Machine (EVM) is its computation
    engine that executes smart contracts. Ethereum allows developers to
    build decentralized applications and is the basis for many web3
    projects. *Example*: ERC-20 tokens, a standard for creating fungible tokens on Ethereum.

### Web3

Web3 is a term 
used to describe the new paradigm of the internet powered by blockchain 
and smart contracts. Unlike the previous versions of the web, web3 is 
permissionless and relies on decentralized networks rather than 
centralized servers. This ushers in an era of censorship-resistant and 
transparent agreements and transactions, often called an ownership 
economy.

**Web1:**

The permissionless open sources web with static content

**Web2:**

The permissioned web, with dynamic content where companies run your agreements on their servers.

**Web3:**

The permissionless web with dynamic content.

- Decentralized censorship reesistant networks run your agreemeent and code.
- User owned ecosystems where one owns a portion of the protocol they interact with - instead of solely being the product

### Wrap Up

We've taken a high-level view of the blockchain landscape, including its history and the problems that smart contracts solve.

At this point you might be asking yourself

*what do these smart contracts really mean?*

or

*what is meant by trust minimized agreements/unbreakable promises?*

In my mind a technology is really only as good as the problem it solves. So next, we're going to look at what the

**purpose**

of

```
smart contracts
```

is - what's the value proposition exactly?

# **Purpose of smart contracts**

## The Essence of Blockchain and Smart Contracts

Almost every 
interaction or transaction in our lives involves some form of agreement 
or contract. For instance, purchasing a chair involves a contract to buy
 lumber, assemble it, and sell the finished product. Your electricity 
supply is also based on an agreement between you and the electric 
company. When you get an oil change for your car, you're promised a 
service in exchange for money.

Almost everything we do in modern life relates to an agreement or contract in some way.

To
 make it more relatable, think of contracts and agreements as promises. 
Traditional contracts, however, require trust between parties, and this 
doesn’t always work in favor of honesty and fairness.

### The Problem with Traditional Agreements

Lets
 consider some real world examples of where trust leverages agreements 
can go wrong and why blockchain technology and smart contracts mitigates
 these risks.

### Consumer Trust

In the 80s and 90s, McDonald’s 
Monopoly game promised customers a chance to win money through game 
cards obtained with purchases. However, it turned out that the game was 
rigged by insiders who manipulated the system for their gain. 
Essentially, McDonald’s failed to keep its promise.

This example demonstrates that relying on trust within agreements can lead to fraudulent activities and broken promises.

With
 smart contracts, we can eliminate the need for trust. A smart contract 
is an agreement or a set of instructions that are deployed on a 
decentralized blockchain. Once deployed, it cannot be altered, it 
automatically executes, and everyone can see its terms.

Imagine if 
McDonald’s Monopoly game was operated on a blockchain through a smart 
contract. The fraudulent activities would have been impossible due to 
the immutable, decentralized, and transparent nature of smart contracts.

### Banking and Trust

Traditional
 banks have sometimes failed to keep the promise of safeguarding 
people's money, as seen during the Great Depression. Blockchain and 
smart contracts can ensure transparency and execute automated solvency 
checks, preventing the bank from becoming insolvent.

The core of 
blockchain and smart contracts lies in creating a trustless system where
 agreements are transparent, unchangeable, and executed without human 
intervention. This technology holds the potential to revolutionize 
industries and everyday agreements by ensuring honesty and fairness.

### Financial Markets Access

Centralized
 bodies, like traditional exchanges, have the power to restrict access 
to financial markets. This was evident when Robinhood restricted trading
 on certain assets in 2021. With decentralized exchanges like Uniswap, 
there is no central authority that can alter or limit market access. 
This introduces fairness and openness to the financial markets.

### To Summarize

- Traditional Agreements: Require trust in a centralized entity.
- Smart Contracts: Transparent, decentralized, and tamper-proof.

In
 a scenario where you have to choose, smart contracts are an obvious 
choice as they cannot be manipulated or altered in anyone's favor.

Smart contracts are

*the*

solution to minimizing the reliance on trust based systems that have historically failed us time and time again.

### Under the Hood

Smart
 contracts are relatively new, but have already started transforming 
various markets. They do this by representing 'promises' as code on the 
blockchain. This code is executed by a decentralized collective, such 
that no single entity can alter the agreemeent in any way! The agreement
 and it's terms are public knowledge and will automatically execute 
without human intervention.

More industries are adopting smart 
contracts and blockchain due to the numerous advantages they offer. This
 results in trust-minimized agreements or what can be simply termed as 
unbreakable promises.

### Beyond Trust Minimization

It is important 
to note that blockchain, smart contracts, and cryptocurrencies are not 
just about trust-minimized agreements. They offer security benefits, 
uptime advantages, execution speed, and

**much more**

.

### Caution: Not All Are Equal

However, beware of platforms that claim to be decentralized but are not in practice. An example from 2022 is the

```
SBF's FTX platform
```

.
 It presented itself as a Web3 platform, but was essentially a 
traditional Web2 company using cryptocurrency without the benefits of 
smart contracts.

As an emerging developer or user in this space, it's
 important to discern between legitimate projects and those that aren't 
contributing to the ethos of Web3. I want you to be successful, but I 
want you to be successful because you're creating value. Platforms like

```
FTX
```

were pretending to bring value to the space and leeching value from it.

### Wrap Up

What
 we've learnt is that traditional contracts or agreements between 
parties are almost always trust based. Trust based agreements come with 
inherent flaws and the potential of broken agreements, the conseequences
 of which we've seen throughout history - The Great Depression, Monopoly
 Lottery, Robin Hood etc.

Blockchain technology and smart contracts 
solve these problems by introducing fairness, transparency and 
immutability to promises. These attributes of smart contracts assure 
that trust isn't required and we can be certain that an agreement will 
be executed as described 100% of the time.

Lastly, it's important to note that there are several actors, such as

```
FTX
```

which

*pretend*

to embody the ideologies of Web3, but are really centralized entities 
looking to extract value from the system, be aware of these.

# **Current smart contract landscape**

## Features of Smart Contracts

Smart contracts come with various features that distinguish them from traditional agreements.

### Decentralization

The
 first feature is decentralization; smart contracts do not rely on any 
centralized intermediary. Instead, they run on a blockchain which is 
maintained by thousands of individuals known as node operators. It's the
 collective effort of these node operators running the smart contracts 
that make the network decentralized. This aspect will be discussed more 
in-depth later.

### Transparency and Flexibility

Transparency is 
inherent to blockchain networks. Since all node operators can see 
everything happening on-chain, there is no room for unfair or hidden 
deals. This transparency ensures that everyone has access to the same 
information and plays by the same rules.

It is important to note that
 this transparency does not necessarily compromise privacy. Blockchain 
is pseudo-anonymous, meaning that your transactions are not directly 
tied to your real-world identity.

### Speed and Efficiency

Smart 
contracts and blockchain transactions are incredibly fast and efficient 
compared to traditional banking systems. For example, bank transfers, 
especially international ones, can take up to several weeks, whereas 
blockchain transactions happen almost instantly. This speed is not only 
convenient but also allows for more efficient interactions between 
parties.

### Security and Immutability

Once a smart contract is 
deployed, it cannot be altered or tampered with. This immutability 
ensures that the terms of the contract are set in stone. This is a stark
 contrast to centralized systems where a server or database can be 
hacked, and data can be altered. The decentralized nature of blockchain 
makes hacking nearly impossible since an attacker would have to take 
control of more than half the nodes, which is significantly more 
challenging than compromising a single centralized server.

Additionally,
 the data on a blockchain is resilient. In a traditional system, if your
 computer and backups fail, you lose all your data. In contrast, in a 
blockchain, your data is replicated across thousands of nodes. Even if 
several nodes were to go down, your data would remain secure as long as 
there is at least one copy of the blockchain.

### Elimination of Counterparty Risk

Smart
 contracts eliminate the need for trust in transactions. Once a smart 
contract is deployed, its terms cannot be changed. This means that 
parties cannot alter the agreement based on greed or any other factors. 
This ensures that the agreement is enforced as originally intended.

In
 traditional systems, there is always a risk that the other party might 
not fulfill their end of the bargain. With smart contracts, this risk is
 eliminated, and agreements are enforced programmatically.

## Applications of Smart Contracts

Smart contracts have given rise to new industries and revolutionized existing ones.

### Decentralized Finance (DeFi)

DeFi,
 or Decentralized Finance, allows users to engage with financial markets
 without relying on centralized intermediaries. With smart contracts, 
users have transparent access to financial markets and can engage with 
sophisticated financial products efficiently and securely. We will 
provide practical examples of how to build and interact with DeFi 
protocols in upcoming lessons.

### Decentralized Autonomous Organizations (DAOs)

DAOs
 are governed entirely by smart contracts and operate in a decentralized
 manner. This structure offers benefits such as transparent governance, 
efficient engagement, and clear rules. DAOs are an evolution in politics
 and governance, and we will cover how to build and work with DAOs in 
future lessons.

### Non-Fungible Tokens (NFTs)

NFTs, or Non-Fungible 
Tokens, can be thought of as digital art or unique assets. NFTs have 
created new avenues for artists and creators to monetize their work. We 
will also cover how to create and interact with NFTs in this course.

### Other Applications

And then, maybe

*you'll*

be the one to discover the next iteration of smart contract applications!

# **How Blockchains work**

In this lesson, we're going to break down blockchains, the process and 
the technology itself using a widely-praised and accessible demo 
available

[here](https://andersbrownworth.com/blockchain/)

.

### Understanding Hash Functions

At
 its simplest, a hash is a unique, fixed-length string that serves to 
identify any piece of data. When you input any kind of data into a hash 
function, it produces a hash. In this demo, the hash algorithm we'll 
focus on is SHA-256.

![https://updraft.cyfrin.io/blockchain-basics/07-how-do-blockchains-work/how-do-blockchains-work1.png](https://updraft.cyfrin.io/blockchain-basics/07-how-do-blockchains-work/how-do-blockchains-work1.png)

If I add

```
Patrick Collins
```

to our

```
SHA-256
```

algorithm, it will:

1. Convert the letters to numbers
2. Convert the numbers to a fixed-length “string” or “hash”

```
Patrick Collins
```

gets converted to

```
7e5b5a1a6b80e2908b534dd5728a998173d502469c37121dd63fca283068077c
```

Ethereum,
 uses its own version of a hashing algorithm (Keccak256)that isn't 
exactly SHA-256 but belongs to the SHA family. This doesn't change 
things significantly here as we're primarily concentrating on the 
concept of hashing.

In the application, whatever data you enter into 
the data section, undergoes processing by the SHA-256 hash algorithm 
resulting in a unique hash.

> For example, when I input my 
name as "Patrick Collins," the resulting hash uniquely represents 
"Patrick Collins." The fascinating aspect is, no matter how much data is
 input, the length of the generated hash string remains constant.
> 

### Understanding Blocks

Now
 that we've grasped the concept of hashing and fixed-length string, 
let's inspect the structure of a blockchain—a collection of "blocks."

![https://updraft.cyfrin.io/blockchain-basics/07-how-do-blockchains-work/how-do-blockchains-work2.png](https://updraft.cyfrin.io/blockchain-basics/07-how-do-blockchains-work/how-do-blockchains-work2.png)

A
 block takes the same data input, but instead of a singular data field, a
 block is divided into 'block', 'nonce', and 'data.' All three are then 
run through the hash algorithm, producing the hash for that block. As a 
result, even a minor change in the data leads to an entirely different 
hash, hence, invalidating the block.

In essence, mining involves the 
computational trial and error process of finding an acceptable value to 
produce a hash which typically follows a certain pattern, such as 
starting with four zeros. The value found, which satisfies this 
criterion, is known as the 'nonce'.

The problem or criteria a miner has to solve will vary from blockchain to blockchain, but the concept is the same.

### The Inherent Beauty of Blockchain: Immutability

In
 a blockchain, which is essentially a sequence of blocks, each block is 
comprised of the previous elements - a block number, a nonce and data - 
as well as

```
the hash of the previous block
```

![https://updraft.cyfrin.io/blockchain-basics/07-how-do-blockchains-work/how-do-blockchains-work3.png](https://updraft.cyfrin.io/blockchain-basics/07-how-do-blockchains-work/how-do-blockchains-work3.png)

What
 this means in practice is that any changes to data, in any block of the
 chain, will invalidate every proceeding block, until they are 
recalculated, or re-mined.

> Genesis Block:
> 

### Decentralized Distribution

Now,
 if a single entity were to control the blockchain, they could 
conceivably change any data they want, and then re-mine, or re-validate 
subsequent blocks. This is bad.

*Enter Decentralized Distribution.*

![https://updraft.cyfrin.io/blockchain-basics/07-how-do-blockchains-work/how-do-blockchains-work4.png](https://updraft.cyfrin.io/blockchain-basics/07-how-do-blockchains-work/how-do-blockchains-work4.png)

The
 crux of blockchain's power lies in its decentralization or distributed 
nature. Under this system, multiple entities or "peers" run the 
blockchain technology, each holding equal weight and power. In the event
 of disparity between the blockchains run by different peers (due to 
tampering or otherwise), the majority hash wins, as the majority of the 
network agrees on it.

Nodes that don't agree with the majority effectively fork the network, continuing on their own with their own history.

### Interplay of Blockchain & Transactions

Until
 now we've been considering the data passed in a block to be a random 
string of text, but the reality is - this data can be anything. In the 
token and coinbase sections of this demo you can see how each block is 
comprised of a number of transactions that all get hashed together. Any 
edits to any of these transactions is going to invalidate the chain!

![https://updraft.cyfrin.io/blockchain-basics/07-how-do-blockchains-work/how-do-blockchains-work5.png](https://updraft.cyfrin.io/blockchain-basics/07-how-do-blockchains-work/how-do-blockchains-work5.png)

### Wrap Up

To
 summarize, every transaction, block, and indeed the whole blockchain 
itself comes down to understanding the concept of a hash—this unique 
fixed-length string that is intrinsically linked with the original data.
 We've also underscored the importance of decentralization and 
highlighted how the concept of immutability plays into the system's 
security.

NB:

A nonce- is a “number used once” to find the “solution” to the blockchain problem.

A Block -  is a list of transactions mined together

Mining - Process of finding the “solution” to the blockchain “problem”

# **Blockchain overview**

### Preface

I'll start by saying, you've done great getting his far,
 if at first some of these concepts are hard to grasp, things will get 
better with experience as we move through the course and you're exposed 
to real world examples.

I definitely would recommend going back and reviewing the parts that you don't quite get and asking questions in the

[**discussions tab**](https://github.com/Cyfrin/foundry-full-course-f23/discussions)

of the GitHub repository.

Now
 that we know all the cryptography pieces, how the blockchain actually 
works, how our signatures work and how everything sticks together, let's
 talk a little bit about how this works in actuality and what's really 
going on.

It's important to note that many of the concepts we've 
covered and will cover are going to pertain to Ethereum, or the EVM 
ecosystem. Each specific blockchain however, may have their own nuances 
and intricies to watch out for. Trust that the overarching concepts will
 all be the same, but keep an eye out for the specific criteria that may
 very from chain to chain, how blocktime is handled, or which hashing 
algorithm is used for example.

### Traditional Networks vs Blockchain

Traditionally,
 when you run an application be it a website or something that connects 
to a server you are interacting with a centralized entity. This is the 
opposite of what you may recall from our distributed blockchain example,
 in that the server is controlled and run by a single centralized group.

Blockchains, as we saw, run on a network of independent nodes. In our previous example, each of the

```
Peers
```

was representative of an independent

```
node
```

operator. The term

```
node
```

typically refers to a single instance of a decentralized system, Peer A would be a

```
node
```

.
 This network, this combination of these nodes interacting with each 
other is what creates a blockchain. What makes these networks so potent,
 is that anybody can join. All anyone needs is a little bit a hardward 
and you can participate in securing a blockchain network. You could go 
to GitHub and start operating a node in a few seconds!

In the 
traditional world applications are run by centralized entities and if 
that entity goes down or is malicious or decides that they want to shut 
off - they just can. They're the ones that control everything.

Blockchains,
 by contrast, don't have this problem. If one node or one entity that 
runs several nodes goes down, since there are so many other independent 
nodes running, it doesn't matter, the blockchain and the system will 
persist so long as there is at least one node always running. Luckily 
for us, the most popular chains like Bitcoin and ethereum have thousands
 and thousands of nodes. Malicious nodes are kicked from the network, or
 even punished in some cases. Majority rules when it comes to the 
blockchain.

This gives blockchains this incredibly potent 
immutability trait where nothing can be changed or corrupted so in 
essence we can think of a blockchain as a decentralized database. In the
 case of Ethereum it has an extra additional feature where it also can 
do computation in a decentralized manner now.

### Consensus

Let's talk consensus. This includes

```
Proof of Work
```

and

```
Proof of Stake
```

. You've probably heard these terms before and they're really important to how these blockchains work.

The

```
mining
```

feature of our previous blockchain example was an example of

```
Proof of Work
```

```
Proof of Work
```

and

```
Proof of Stake
```

fall under this umbrella of

```
consensus
```

and

```
consensus
```

is a really important topic when it comes to blockchains.

> Consensus
> 

Very
 roughly, a consensus protocol in a blockchain or decentralized system 
can be broken down into two pieces a chain selection algorithm and a 
sybil resistance mechanism. Mining, or Proof of Work, is a sybil 
resistance mechanism. This is what Bitcoin currently uses.

```
Proof of Work
```

is known as a sybil resistance mechanism because it defines a way to 
figure out who is the block author or which node did the work to mine a 
block. Sybil resistance is a blockchain's ability to defend against 
users creating a large number of pseudo-anonymous identities to gain a 
disproportionately advantageous influence over said system.

As mentioned, there are two primary types of sybil resistance:

- Proof of Work
- Proof of Stake

We'll look a little closer at

```
Proof of Work
```

first.

### Proof of Work

Proof
 of work is a system of sybil resistance used in many blockchains, in 
its essence a miner needs to go through a very computationally heavy 
process (mining) to find the block's answer. As a result, it doesn't 
matter how many additional nodes you're running, each node is obligated 
to do this work in order to receive a reward. The playing field is kept 
fair.

> Note:
> 

Proof of Work needs to be combined with a

```
chain selection rule
```

to create

```
consensus
```

.

A

```
chain selection rule
```

is implemented as a means to determine which blockchain is the

*real*

blockchain. Bitcoin (and prior to the merge, Ethereum), both use something called

```
Nakomoto Consensus
```

. This is a combination of Proof of Work (Etherum has since switched to Proof of Stake) and the

```
longest chain rule
```

.

In the

```
longest chain rule
```

, the decentralized network decides that whichever chain has the most number of blocks will be the valid, or

*real*

blockchain. When we saw

```
block confirmations
```

in Etherscan earlier, this was representing the number of blocks ahead of our transaction in the longest chain.

> You'll sometimes hear people use
> 
> 
> **Proof of Work**
> 
> *and*
> 

```
Proof of Work
```

also serves as a means to determine who receives transaction fees as we
 discussed earlier. These transaction fees are paid by whomever 
initiates the transaction. In a Proof of Work system, every node is 
competing against eachother to solve the block problem first. The first 
node to solve the problem gets paid the transaction fees accumulated in 
the block they mine. In addition to this, miners are also paid a

```
block reward
```

, the

```
block reward
```

is given by the blockchain itself.

> If
 you've previously heard of the Bitcoin Halving - this is the concept of
 the block reward being cut in half roughly every 4 years.
> 

Block
 rewards are in the blockchains native currency - Bitcoin = BTC, 
Ethereum = ETH. This effectively increases the amount of that 
cryptocurrency in circulation.

### Blockchain Attacks

There are two major types of attacks that exist in the blockchain space.

- Sybil Attack - When a user creates a number of pseudo-anonymous accounts to try to influence a network.
- 51% attack - Occurs when a single entity possesses both the longest chain
and majority network control. This would allow the entity to `fork` the chain and bring the network onto the entities record of events, effectively allowing them to validate anything.

Blockchains are very democratic. The bigger a blockchain is, the more decentralized, the more secure it becomes.

I encourage you to look into running a node yourself to increase the security of the network!

Proof
 of Work does come with drawbacks. For example, Proof of Work consumes a
 LOT of electricity. When you have thousands of nodes all working as 
hard as they can to solve a block problem the energy consumption is HUGE
 and as such, so is the potential environmental impact.

With the 
above in mind, many protocols are choosing the shift to a different 
consensus mechanism that is more environmentally friendly. The most 
popular of which is...

### Proof of Stake

In contrast to trying to 
solve a block problem, Proof of Stake nodes put up some collateral that 
they are going to behave honestly aka they

```
stake
```

. If a node
 is found to be misbehaving, it's stake is slashed. This serves as a 
very effective sybil resistance mechanism because for each account, the 
validator needs to put up more stake and misbehaving risks losing all 
that collateral.

> In a Proof of Stake system,
> 
> 
> ```
> miners
> ```
> 
> ```
> validators
> ```
> 

Unlike
 in Proof of Work, where each node is racing to solve the block problem 
first, in Proof of Stake, validators are pseudo-randomly chosen to 
propose the next block and other nodes will validate it.

Proof of Stake of course comes with its own Pros and Cons.

Pros:

- great sybil resistance mechanism
- great for the environment, much less energy

Cons:

- seen as less decentralized due to upfront staking costs

This raises the question of

*how decentralized is decentralized enough?*

and I think I need to leave that to the community to decide.

### Layer 1 and Layer 2

I want to briefly touch on the concepts of Layer 1 and Layer 2 networks here as well.

1. `Layer 1` solutions: This refers to base layer blockchain implementations like Bitcoin or Ethereum.
2. `Layer 2` solutions: These are applications added on top of a layer one, like [Chainlink](https://chain.link/) or [Arbitrum](https://arbitrum.io/).

Layer
 2s like Arbitrum and Optimism are special in that they're trying to 
solve the problem of scalability. These protocols leverage something 
called

```
rollups
```

. We won't go too deep, but the idea is that the protocols bundle their transactions to be processed by a Layer 1.

### Wrap Up

This
 overview was huge. Amazing work, you now have a fundamental 
understanding of how blockchains work, how to interact with them and why
 they're so secure and empowering.

# A simple onion architecture model

**First of all, why this repo?**   
Well, to answer a very singular question: How can we have codebases that are easy to maintain, extend and still have the ability to increase performance later when those scaling headaches come. 

An Onion architecture is built on a domain model in which layers are connected through interfaces. The idea is to keep external dependencies as far outward as possible where domain entities and business rules form the core part of the architecture.

There are many variations and ways of implementing a standard onion model.
But we are going to take a look at a very simple one 

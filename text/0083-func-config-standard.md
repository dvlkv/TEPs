- **TEP**: [0](https://github.com/ton-blockchain/TEPs/pull/0)
- **title**: FunC project configuration file
- **status**: Draft
- **type**: Meta
- **authors**: [Danila Volkov](https://github.com/dvlkv), [Andrey Pfau](https://github.com/andreypfau)
- **created**: 15.08.2022

# Summary

I propose to make a FunC project config, like project.json, Cargo.toml, etc.

# Motivation

Extensions, compilers and other dev tools need universal project configuration.

# Guide

Extensions can use it for optimal indexing source code, compilers can be configured without bash scripts.  
Also, here comes more convinient project bootstapping. 

# Specification

I suppose it should be yaml file, named like .func.yml or something else.
In first implementation it should contain:
- root source folder
- entrypoints (contract root files), relative to source folder
- (optional) library directories
- (optional) compiler configuration (version, etc.)  

Example file looks like:
```yml
сompiler: 
    version: 0.2.0
sources: src/
entrypoints:
    - contracts/nft.fc
    - contracts/nft-collection.fc
libraries:
    - node_modules/func-*
```

# Drawbacks

Existing tools with configuration files should be adopted to work correct with this format.

# Rationale and alternatives

- Why is this design the best in the space of possible designs?

In this implementation, configuration file contains only generic information without domain-specific data.

- What other designs have been considered and what is the rationale for not choosing them?

Disintar's [ton-cli](https://github.com/disintar/toncli/blob/master/docs/advanced/project_structure.md) configuration file was suggested to use, but it has obvious cons: domain-specific required fields, every contract description, obsolete lists of files included in contract.

- What is the impact of not doing this?

Development experience struggles from absence of single configuration file. Different tools will require different configuration files.

# Prior art

Ethereum's hardhat has a [configuration file](https://hardhat.org/hardhat-runner/docs/config), there you can specify networks, project directories and compiler configuration. Having configuration like this in TON makes development easier. Proposed configuration format is simple and extensible. Tools can add their custom configuration fields without any problems.

# Future possibilities

With involvement of the ecosystem, config can be extended, as mentioned before in *Prior art* section. If the compiler gets configurable properties, they can be added to the `compiler` section, if the tool used by developer needs additional configuration, it might be done in section with custom name.

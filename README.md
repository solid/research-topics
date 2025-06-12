## What is this repo?

A set of research topics that affect Solid in some way. Designed to be a point of insipiration and a starting point for discussion on many of those topics.

In an ideal case, each topic will take on a life of its own and have a repository dedicated to work on it.

## Status

To get us started this is a dump of topics in a single file - the goal is to make this more structured in time.

## Topics

### Data governance and Solid
There is a need to make Solid easier for Industry and Governments globally to adopt within their [**Enterprise Data Governance (EDG)**](https://www.sap.com/products/technology-platform/master-data-governance/what-is-data-governance.html) and broader [**Enterprise Information Governance (EIG)**](https://www.nyu.edu/life/information-technology/data-services-and-analytics/global-privacy-and-data-strategy/enterprise-information-governance-and-management.html) strategies. The research challenge within *academia* and *industry* to add **automated EDG support** to Solid. In academia, [Harshvardhan J. Pandit](https://harshp.com/) at [Dublin City University](https://www.dcu.ie/) and [Beatriz Esteves](https://www.linkedin.com/in/beatriz-esteves-032249156/) at [SolidLab](https://solidlab.be/) have expertise with [ODRL](https://www.w3.org/TR/odrl-model/) and [DPV](https://w3c.github.io/dpv/2.0/dpv/) which may be key components of a semi-automated data governance layer for Solid. In the Dataspace Community [**IDSA**](https://internationaldataspaces.org/) uses [ODRL](https://www.w3.org/TR/odrl-model/) as a [key component](https://docs.internationaldataspaces.org/ids-knowledgebase/dataspace-protocol/overview/terminology#agreement) of [their standard](https://docs.internationaldataspaces.org/ids-knowledgebase/dataspace-protocol) to establish agreements for [sharing datasets](https://docs.internationaldataspaces.org/ids-knowledgebase/dataspace-protocol/overview/terminology#dataset) \- and thus would be a valuable partner. EIG, a superset of EDG, must be carefully considered. With [infrastructure providers for Solid](https://solidproject.solidcommunity.net/catalog/) acting as [Data Trusts](https://theodi.org/insights/explainers/what-is-a-data-trust/), and an expectation that **government** and **enterprises** migrate to read/write personal data from Pods, there is a need to proactively provide support for these organisations to manage the implications for their EIG strategies. In particular, we need to create a generic, Solid compatible, EIG strategy. Josh Cornejo recently presented some work around this topic to the Solid Practitioners channel in [https://spectra.video/w/21t7aswEMXkUCjzHsB8CLa](https://spectra.video/w/21t7aswEMXkUCjzHsB8CLa).

There is lots of technical and non-technical research to be done around this. To get a flavour of such research see [this proposal](https://docs.google.com/document/d/1Ilh5H2IkBWeeRVMMtRSrIQ0_w-nBOyZo/edit).

### Platforms on top of Solid
There are many platforms that can be built on top of Solid, that may be research projects of their own right, or be built as part of other projects.

- Research and data analytics platforms on top of Solid such as a platform for researchers to define the parameters of a dataset they need to do, e.g. population analysis, or to virtualise datasets to train ML algorithms. I would that that of interest to some of the research team at the Open Data Institute would be to have a platform that generates ML training sets annotated [Croissant metadata](https://research.google/blog/croissant-a-metadata-format-for-ml-ready-datasets/).  
- Consent collection/management platform similar to [ConsentKit](https://consentkit.com).

### Privacy Enhancing Technologies & Solid

- Using zero-knowledge proofs for automated data-minimisation when sharing. Zero knowledge proofs can enable *selective disclosure* and *derived disclosure* of signed data. Selective disclosure is sharing a subset of signed attributes, derived disclosure is proving that a property can be derived from a set of signed facts (e.g. I can prove that I am over 21 to a bar using a government signed statement about my DOB, without disclosing my DOB to the bar). Whilst both are used heavily in modern digital wallet solutions, usually as part of [Verifiable Credentials](https://www.w3.org/TR/vc-data-model-2.0/) \- however, there is currently lots of custom code that needs to be written to perform and verify the derivation. It would be useful to Solid and a range of other efforts to be able to generate derived data \+ proof on demand when data is query (e.g. deriving age \+ proof from DOB \+ signature when querying for foaf:age in a database).
   - **Jesse Wright (@jeswr) has started work on this topic at [https://github.com/jeswr/queryable-credentials](https://github.com/jeswr/queryable-credentials)**.  
- End to End Encryption (E2EE): Concerns are often raised about the need to have a Solid Resource Server take responsibility for managing all of the work around, e.g., disk encryption for resource storage. Here, trust is required on two fronts: guarding against the resource server does not have poor (or malicious) security practises that results in data being leaked to other malicious actors, and trusting that the resource server does not tamper with the data served back to applications. E2EE is a method for resolving this whereby the sender encrypts data before transmitting it to servers, and then ensures that only those actors with permission to read the data can do so. Important questions here are:  
  - How should key management be performed so as to ensure that only those actors with access to the resource can modify it  
  - Can, e.g., FHE be used to retain support for server-side query over RDF data. Related work ([https://link.springer.com/chapter/10.1007/978-3-319-58068-5\_37](https://link.springer.com/chapter/10.1007/978-3-319-58068-5_37), [https://ieeexplore.ieee.org/abstract/document/9458850](https://ieeexplore.ieee.org/abstract/document/9458850), [https://link.springer.com/article/10.1186/s13326-017-0112-6](https://link.springer.com/article/10.1186/s13326-017-0112-6), [https://content.iospress.com/articles/semantic-web/sw180335](https://content.iospress.com/articles/semantic-web/sw180335), [https://www.semantic-web-journal.net/system/files/swj1733.pdf](https://www.semantic-web-journal.net/system/files/swj1733.pdf))
  - **Henri Cattoire developed an extension to the Solid protocol that enables E2EE through Attribute-Based Encryption, along with a proof-of-concept application. The source code is available at [https://github.com/henricattoire/solid-e2ee](https://github.com/henricattoire/solid-e2ee).**  
- Current PDS approaches have limited support for ensuring privacy when computations combine data spread across users. [Secure Multi-Party Computation (MPC)](https://www.cs.ox.ac.uk/publications/publication16239-abstract.html) is a well-known subfield of cryptography, enabling multiple autonomous parties to collaboratively compute. Whilst Oxford has already done some work investigating SMPC with Solid, there is work to be done to see what affordances / adjacent specs (for instance for server \<-\> server exchange) to allow users to query for the results of an MPC computation, and for the servers to execute that computation. There is a follow up set of research on **governance** and **policies** to understand how to, e.g. express the fact that you’re willing for your salary to be included as part of an *average* for an economic study, but not for that salary to be directly disclosed to anyone.

A potential research proposal related these topics can be found [here](https://github.com/solid/research-topics/blob/main/privacy-preserving-query.pdf)

### Aggregators / Indexes

Ideally, the following use cases should be enabled:
 - I want to be able to query all public triples across all Pods on the web from a single endpoint
 - I also want to be able to query across some protected triples when providing authentication to the indexing service either because:
   - The aggregators is a trusted intermediary for handling private data
   - E2EE encryption is used so that the aggregator does not need to be trusted

In both cases, ideally provenance would be available to prove the integrity of the data in the aggregator without needing to trust said aggregator.

@jacksoncreed has [these slides](./SearcherCentricSearch.pdf) on the topic.

### Interfaces on top of aggregators

 - WebId search: Discover the WebId of someone I know

### Web Agents

- Building specifications for (Semantic) Web agents that operate over Pods  
- Resolution mechanisms for agents operation on different logical assumptions  
- Collaborate on emergent research on LLMs looking up external data as part of their evaluation process (this is *not* RAG, it is architecturally building data lookup into the LLM) 

### Data management

- [CRDTs](https://en.wikipedia.org/wiki/Conflict-free_replicated_data_type) (conflict-free replicated datatypes) support local-first and collaborative application by providing resolution mechanisms . A W3C community group has been established to work on the development of [RDF specific CRDT algorithms](https://www.w3.org/community/crdt4rdf/). 

### Private Data and LLMs

- There is a range of technical and research work to be done around knowledge graphs, private data and LLMs. On the more technical front there is work to do such as implementing the [Model Context Protocol](https://www.anthropic.com/news/model-context-protocol) for Solid. Also note that perplexity acquired [Carbon](https://www.perplexity.ai/hub/blog/welcoming-carbon-to-the-perplexity-team) to provider similar functionality to LLMs.

  On the more research side, there is work to e.g. see if we should be adding vector database type access to Solid, and whether, e.g., we can be assigning entities points in vector space and doing similarity searches on entities. What applications can be built on top of this?

### Tooling to assist data management

- A tool to warn me of potential outcomes \- especially harmful outcomes \- of changing data, or permissions on data. For instance, warn me that I might my Visa to live in the UK if I change my address to an Australian address for more than 3 months \- because the immigrations office has access to that address.

### Developer Experience

- There is extensive work on tooling for RDF, with varying degrees of abstractions and interaction patterns. Just a few of such abstractions can be found at [https://rdfjs.dev/](https://rdfjs.dev/); yet we still aren’t at the point where way can say “Hey, so you’re a front end developer you want to build a Solid application in Domain X, here is how you can get up and running in only 2 hours; and not have to worry about data modelling or management, that’s all handled”. We need to get to that point for Solid in order to get a critical mass of developer building Solid applications.

### Design Patterns

- Part of the reason that Solid lacks good educational materials for many topics, is a result of a lack of generally accepted design patterns to solve many challenges. This includes:  
  - Standards for provenance, and provenance validation. There are many scenarios in which services and applications need to establish a basis on which they can trust \- such as having the data signed by a trusted organisation. Currently there are no well-accepted standards for how to sign and verify such data in Solid.  
  - Best practices for data access requests. Access requests have been implemented in multiple ways across different projects and servers. There is a need to critically evaluate the different design patterns and propose a single flow as a use-case.

### Social Science Research

- What do people want the future of their technologies and online experiences look like?  
- Downstream effects of amendments to data:  if he were to update that address in Solid, and DVLA had access \- what would the impact of that be? (*Note that this complements the development of the tooling to assist data management*).

**Understanding the context in which we are building Solid**

- How does Solid relate to the concept of a [data mesh](https://www.datamesh-architecture.com). Is there feature parity? What are the gaps if any?

### What data can I trust?

- Just as with the Semantic Web “anyone can say anything about anything”, so just as with the Web, you cannot take every piece of information in everyones Pod to be true. How can applications use provenance (computational trust) \+ assumptions / guarantees of what entities are trustworthy to establish what data to “believe” for a given application. To put it another way, can I execute a SPARQL query, which evaluates over data deemed “trustworthy” based on the provenance presented, and trust assumptions given to the query engine.

### Ontology Creation

- Automated ontology creation with LLMs: There is research taking place to [Map the Mind of Large Language Models](https://www.anthropic.com/research/mapping-mind-language-model) \- with this, there is an opportunity to automatically create ontologies for new or niche domains. This is done by generating an approximate logical representation of the conceptual worldview encoded in LLMs.

### Data Generation

- Automated data creation with LLMs: Many companies are now having commercial success in generating Knowledge Graphs from unstructured, or semi-structured documents such as PDFs. There are a range of research projects to make systems that convert existing data sources into structured RDF to use with applications.

### Related to / extending existing work in academia

- Working on the development of Malleable Software on top of Solid. Malleable Software was the topic of [Geoffrey Litt](https://www.geoffreylitt.com)’s PhD at CSAIL \- I’m not sure if there is anyone currently working on this topic in CSAIL, it looks like Prof. Daniel Jackson might be with his [Wildcard](https://www.csail.mit.edu/research/wildcard) project and Prof. David Karger is interested in such topics with [Mavo](https://www.csail.mit.edu/research/mavo-creating-interactive-data-driven-web-applications-authoring-html). There has long been an item on the Solid Roadmap to integrate Solid with Malvo as a research item in the Solid Ecosystem roadmap.
  - Work so far: Syntropize https://syntropize.com is a proof-of-concept malleable software operating environment by Rahul Gupta that uses Solid PODs when storing data online.
- Collaboration with [TrustNet](https://www.technologyreview.com/2024/08/27/1095980/a-tool-that-lets-users-fight-misinformation-online/) to capture the accuracy of data in Pods, (e.g. in my Pod I make statements about the accuracy of other people's data in their Pod). Is quite a core challenge that needs to be solved. Can be applied to content accuracy for decentralized Social media on top of Solid, filtering out poor data when doing federated queries to collect research data, etc.  
- Adding Solid storage as a feature to the [MIT App Inventor](https://appinventor.mit.edu) Project.  
- Collaboration with [Data Garbling](https://www.csail.mit.edu/research/data-garbling-computing-encrypted-data) project in order to work on the E2EE work items [described below](#bookmark=id.n9myutgtai1n), in particular on topics such as using FHE to support enable SPARQL queries over encrypted data. There may also be some interest related to this coming from those working on [Splintr](https://www.csail.mit.edu/research/splinter-practical-private-queries-public-data), who focus on ensuring that those querying data don’t accidentally disclose information based on the content of their query.  
- Adding features of [squadbox](https://www.csail.mit.edu/research/squadbox-combating-online-harassment-using-friendsourced-moderation), and more generally, implementing completely decentralised moderation for media and social media applications in Solid by allowing users to make statements about how they rate / moderate / endorse / dispute content that other users have put on their Pod, and use this to feed my algorithmic view of the world based on who I want to listen to as moderators and who I don’t.



# IR Models

- **Modeling** in IR is a complex process aimed at producing a ranking function
    + **Ranking function** : a function that assigns scores to documetns wtih regard to a given query

- This process consists of two main tasks:
    + The conception of a logical framework for representing documents and queries
    + The definition of a ranking function that allows quantifying the similarities among documents and queries

# Modeling and Ranking
+ IR systems usually adopt **index terms** to index and retrieve documnets
- Index term:
    + In a restricted sense: it is a keyword that has soime meaning on its own; usually plays the role of noun
    + In a more general form: <mark>it is any word that appears  in a document</mark>
+ Retrieval based on index terms can be impolemented efficiently
+ Index terms are simple to refer to in a query
+ Simplicity is important because it reduces the effort of query formulation

An **IR model** is a quadruple [D,Q,F, R(${q_i,d_j}$)]

1.D is set of logical views for the documents in the collection

2.Q is a set of logical views for the user queries

3.F is a framework for modeling documents and queries

4.R(${q_i,d_j}$) is a ranking function


### Classic IR Models
+ Boolean
+ Vector
+ Probabilistic

### Set Theoretic
+ Fuzzy
+  Extended Boolean
+  Set-based

### Algerbratic
+ Generalized Vector
+ Latent Semantic Indexing
+ (Distributional Representation)

### Probabilistic
+ BM25
+ Languange Model









# Contrasting lexical and sematic representations

Lexical representation (term vector)

+ High-dimensional (billions)
+ Sparse
+ Term vectorm model
+ Words are uninterpreted tokens
+ Computationally cheaper
+ Easy to scale inverted index
+ No explicit language model (caveat :pre & post retrieval)

Sematic representa(embedding):
+ Low dimensional (hundreds)
+ Dense
+ Distributional semantic
+ Words have meaning
+ Computationally more expensive
+ Harder to scale nn-index
+ Updating language model very expensive





# Classic IR Models

## Basic Concepts

+ Each document is represented by a set of representative keywords or index terms
+ An index term is a word or group of consecutive words in a document
+ A pre-selected set of index terms can be used to summarize the document contents
+ However, it mightbe interesting  to assume that all word are index terms(full text representation)

The vocabulary V , is the set of all distinct index terms in the collection

**patterns of term co-occurrences**

# The Boolean Model

**set theory**

Simple model based on **set theory** and **boolean algebra**

- Queries specified as boolean expressions

  + quite intuitive and precise semantics

  + neat formalism

  + example of query

${q = k_a \land (k_b \lor \lnot k_c) }$


+ ${w_{ij}}$:weight associated with pair (ki,dj)

+ ${w_{iq}}$:weight assiciated wtih pair(ki,q)

+ A term conjunctuve component that satisfies a query q is called a **query conjunctive component** c(q)

## Drawbacks of the Boolean Model
+ Retrieval based on binary decision critiria with no notion of pertial matching
+ No ranking of the documnets is provided(absence of a grading scale)
+ Information need has to be translated into a Boolean expression, which most users are most often too simplistic
+ The model frequently returns either too few or too many documents in response to a user query





## Term Weighting

the document frequency ${n_i}$ of a term ${k_i}$ is the number of documnets in which it occurs 

+ There are properties of an index term which are useful for evaluating the importance of the term in a document
    - For instance , a word which appears in all documents of a collection is completely useless for retrival tasks
+ To characterize term importance, we associate a weight ${W_{i,j}}$ with each term ${k_i}$ that occurs in the document ${d_j}$
    -If ${k_i}$ that does not appear in the document ${d_j}$ , then ${w_{i,j} = 0}$


## TF-IDF Weights
- TF-IDF term weighting scheme
    + Term frequency(TF)
    + Inverse document frequency(IDF)
    + Foundations of the most popular term weighting scheme in IR




# Set Theoretic IR Models
+ Set-Based Model
+ Extended Boolean Model
+ Fuzzy Set Model






### Termsets

The fundamental idea is to use  <mark>mutual dependencies</mark>
among index terms to improve results

${S_i}$ = {${k_a , k_b , ... , k_n}$} is a subset of the terms in the collection


### Ranking Computation

+ The ranking computation is based on the vector model, but adopts termsets instead of index terms

+ Given a query **q** ,let
> {S1,S2,S3,S4 ...} be the set of all termsets originated from q

> ${N_i}$ be the number of documents in the collection

> N be the total number of documents in the collection

> ${F_{i,j}}$ be the frequency of termset ${S_i}$ in documnet ${d_j}$

The  the set ${V_s}$ vocabulary-set of the collection

+ The ranl of ${d_1}$ , we need to consider the seven termsets ${S_a,S_b,S_d,S_{ab},S_{bd}}$ and ${S_{abd}}$
+ The rank of ${d_1}$ is then given by 

${sim({d_1,q})}$ = dotproduct / ${\vec{｜d_1｜}}$



A documnet ${d_j}$ and aquery q are represented as vectors in ${2^t}$

The rank of ${d_j}$ to the query ${q}$ is computed as follows

### Closed Tersets
+ The concept of frequent termsets allows simplifying the ranking computation
- Yet there are many frequenct termsets in a large collection
    + the number of termsets to condsider might be prohibitiively high with large queries

+ To resolve this problem , we can further restrict the tranking computation to a smaller number of termsets
+ This can be accomplished by observing some of properties of termsets such as the notion of **closure**

+ The **closure of a terset** ${S_i}$ is the set of all frequent termsets that co-occur with ${S_i}$ in the same set of docs
+ Given the closure of ${S_i}$ the largest ternset in it is called a **closed termset** and is referred to as ${\phi_i}$


# Extended Boolean Model


In the boolean model , no **ranking** of the answer set is generated

One alternative is to extend the Boolean model with the notions of **partial matching** and **term weighting**

This stragy allows one to combine characteristics of the Vector model with properties of Boolean algerba



Then , the closed termset ${S_a}$

sim( ${d_1}$ , q)= ${\frac{\vec{d_j}*\vec{q}}{|{\vec{d_j}}|* {\vec{|q|}}}}$


${c_{i,l}}$ ~ v1

### The Idea 

+ Consider a conjunctive Boolean query given by ${q = k_x \land k_y}$

+ For the boolean model, a doc that contains a single term of ${q}$ is as irrelevant as a doc that contains none
+ However , this **binary decision** criteria frequently is not in accordance with common sense


# Fuzzy Set Model

### Fuzzy Set Model

+ Matching of a document to a query terms is approximate or vague
+ This **vagueness** can be modeled using fuzzy framework, as follows:
    - each query term defines a **fuzzy** set
    - each doc has a **degree of membership** in this set

+ This interpretation provides the foundation for many IR models based on fuzzy theory
+ In here,we discuss the model proposed by Ogawa,Morita,and Kobayashi

+ Fuzzy set theory deals with the representation of classes whose boundaries are not well defined
+ Key idea is to introduce the notion of a **degree of membership** associated with the elements of the class
+ This degree of membership varies from 0 to 1 and allow modeling the notion of **marginal** membership
+ Thus , membership is now a **gradual** notion, contrary to the crispy notion enforced by classic Boolean logic



In the context of Information Retrieval (IR) models, the terms "gradual notion" and "crispy notion" refer to different ways of representing the relevance of documents to a query. These concepts help describe how documents are ranked and retrieved based on their relevance to a user's search query. Let me explain both notions:

Gradual Notion:

The gradual notion is also known as "graded relevance" or "fuzzy relevance." It acknowledges that documents can have varying degrees of relevance to a query.
In a gradual notion model, documents are not simply classified as relevant or non-relevant. Instead, they are assigned a relevance score or degree. This score indicates how well a document matches a user's query. These scores can range from 0 (completely irrelevant) to 1 (completely relevant), with values in between indicating partial relevance.
In a ranked retrieval system using the gradual notion, documents are typically ranked based on their relevance scores in descending order. Users might be presented with a ranked list of documents, where the most relevant ones appear at the top.
Crispy Notion:

The crispy notion is also known as "binary relevance" or "hard relevance." It follows a more traditional approach where documents are classified into two categories: relevant or non-relevant.
In a crispy notion model, documents are treated as either entirely relevant or entirely non-relevant with no intermediate levels of relevance.
In this model, documents are typically ranked based on binary decisions. Documents that meet specific criteria for relevance (usually determined by a predefined threshold or algorithm) are considered relevant and included in the search results. Non-relevant documents are excluded.















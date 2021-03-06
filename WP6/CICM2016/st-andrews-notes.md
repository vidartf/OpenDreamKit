
Need for interoperability to enhance discovery potential, reduce costs in enabling that potential, increase sustainability and reliability of the efforts. 

The goal of this article is to survey some of the current systems, present the MMT system for interoperability of mathematical theories, and outline the solutions it would provide. 

The selection here is heavily biased by the OpenDreamKit project. 


 St Andrews report     http://opendreamkit.org/meetings/2016-01-25-DKS/report/

# FindStat


Overview at a high level of your system
FindStat is a database and a web interface accessing the database designed for combinatorists. The purpose is to store and search informations on statistics over combinatorial objects.
A statistic is mostly a map between a set of combinatorial objects to the natural numbers. As an example, the number of edges is a statistic on graphs. The main purpose of FindStat is to give an interface for one to search for some statistics the same way one would search for integer sequences on oeis.

What data do you have?
Structure
We have basically 3 categories of objects.

The combinatorial collections FindStat stores a list of combinatorial collections: 18 as of today (January 2016). All our combinatorial collections are actually linked to a Sage combinatorial collection. We store the minimal informations for us to print the collection on our website and recreate the collection in Sage.

For every collection, we store a list of combinatorial objects. More precisely, we use Sage to generate the list of objects, but we store a standardised version of the printout of the object. This standardised version is homemade: it has to be

standardized: a single given graph will always be printed the same way,
unique: two different graphs will never be printed the same way,
human readable: when possible, it should be easy to understand for a Human reader and not only a machine (so no hashkey or anything like this). When possible, we keep the default printout of Sage object. Sometimes, we have to store a little bit of code to convert this printout into a Sage entry.
The statistics A Statistic is a list of couples : combinatorial object from a certain collection / value. As of now, we have 364 statistics, each of them containing between 200 and 1000 entries. For each statistic, we store some metadata: Name, identifier (specific to FindStat, can be referenced from outside), combinatorial collection, description, code, references, etc. And we also store the data itself: a list of entries, each entry is made from combinatorial object (as a string, by its standardised printout) and a integer value. As an example, the values of "The number of Edges of a graph" St000081 is a list of all graphs up to size 6 with their associated number of edges.

The combinatorial maps A combinatorial map is a mathematical function from a combinatorial collection to another combinatorial collection. For example: binary search tree insertion turns permutations into binary trees. As of now, we store 107 maps each of them containing between 200 and 1000 entries. We store the metadata of the map: domain, codomain, description, code, etc. And we store the mapdata as a list of (value, image) where value and image are combinatorial objects stored as strings through their standardised printout.

As an addition, we also provide some wiki pages with informations on combinatorial objects, maps and statistics in a less formalized way.

Format
Our low level data format is a SQL database where we store everything we need. Most of the data described above is accessible through the website in HTML. All information about statistics and maps can be accessed through json files that have standardised url depending on the identifier of said statistics or maps. It is possible that the url changes if the website organisation is changed in the future but it will always be related to the identifiers which are set once and for all. The format of the json files are also likely to change but we try to limit those changes and keep backward compatibility as much as possible. Those json files are the closest we have to an external API, their are used by the Sage FindStat interface.

All our data are distributed under Creative Commons Attribution-ShareAlike 3.0 Unported License.

How is it produced?
How is it changed?
The data are produced and changed through user contributions. As for now, 55 people are listed as contributors. We have an HTML form to submit statistics where the user receives many informations on what should be submitted and in what format. Once a new statistic is submitted or a change is proposed, it has to be validated by one of the FindStat developers. We don't receive that much data so the process is usually very quick. Each change is stored and so we have access to the full history of the statistic informations with authors.

For maps, we don't have yet the "Add Map" form. Each map has to be added by one of the FindStat developers. The reason is just that the maps are a more recent addition and so the adding process has not been finalized yet.

How do you document it?
We have a very basic documentation for statistic data that we provide to the user who which to contribute. We don't have any documentation for our dataformat (json files).

What knowledge do you have?
Sources of external knowledge?
We relate on the knowledge of our contributors about statistics and maps and try to store it. We also depend on some Sage algorithms, for example to generate the combinatorial objects.

Can you point to implicit knowledge? Is it common knowledge?
Our website is targeted at combinatorists. Even though, we try to give all the basic definitions and information, it might be difficult to use for someone who has no knowledge of these objects.

What would you gain if it was made explicit/machine actionable?
At the moment, our infrastructure is really Sage oriented (object printouts, names, etc). A language-neutral description of our objects might make it easier for interfaces from other system to appear. The gain for us is that the more user we have (from different background), the more contributors we might get and so the more mathematically pertinent our database is.

Have you gone in this direction? How did you represent the knowledge then?
Giving access to the statistics and maps data as json files was a first step in this direction.

How do you collaborate on knowledge representation?
By referencing those data (statistics and maps) and proposing unique identifiers that can be referenced from the outside (the same way the OEIS identifies integer sequences with a unique number).

What software do you have?
What custom software are you running?
We need the software Sage to run some computations: basically, generating the objects, printing them, etc. The statistic and maps code are usually given into Sage for consistency but it is not mandatory.

There is also some FindStat specific code to run the website. Most of this code is just basic webprogramming views of our database.

The database search is the heart of the service. It is a small algorithm that takes a user given statistics and compares it to the database up to some maps.

In which language?
Our server runs on Sage with some imported web packages, so it is written in python. We use the python wiki server MoinMoin as a backend and have written some customized MoinMoin pluggings to run our service.

How does it use the data and the knowledge?
The data is stored in a SQL database. It is preloaded and precomputed when we launch the server then all computations are made on this preloaded data. We don't use the knowledge at this stage, we just basically request the database and compare numbers using some parameters. In the future, we might wanna use the knowledge we have on the maps (bijection, injection, surjection, involution, etc) to improve our algorithm.

How does your software act on represented knowledge?
The software might put into light some mathematical relations between combinatorial objects but doesn't store them or anything like this.

Mixing (revisit?)

Which knowledge is implicit in the data you have?
Which knowledge is implicit in the software you have?
Anything else?



# LMFBB


Overview at a high level of the LMFDB system

The L-functions and Modular Forms DataBase aims to aggregate and integrate computational and mathematical knowledge about L-functions and other number theoretic objects, and to present these complex and interconnected objects reliably while maintaining accessibility. At a mathematical level, this could help provide a uniform view of the concept of L-function, objects which can (sometimes conjecturally) be produced out of very different mathematical constructions. The collaboration involves around 50 mathematicians of varying coding skills and with different mathematical expertise.

What data do you have?

The entirety of the data held by the LMFDB is accessible through an API. One counts around 30 different types of objects stored, for a total of a few TB. The data is downloadable here.

Structure

The data is held in a Mongo database server, holding around 30 or so databases, each with their own collections.

Format

The data is held in the database as BSON (binary JSON), the internal format of Mongo documents.

How is it produced?

Data that ends up in the LMFDB has many different origins. Some are historical computations. Most are done in either GAP, Pari, Sage, Magma, etc, with the person who coded these original sources a member of the LMFDB who aims to make their data more accessible to their peers. Some of the data shown on the website is actually computed on the fly.

Data comes in through a variety of ad hoc ways, but essentially always transits through a JSON format before upload to the Mongo database. At some point there was discussion of allowing anyone to upload their data through an online form. This option is still there, but sees little use.

In general, proper referencing of data sources and documentation of its quality is a struggle.

How is it changed?

Updating is mostly done through some form of overwriting.

How do you document it?

The various formats are in the process of being formalised. The most advanced example is on elliptic curves. The formalisation format itself does not have a spec.

What knowledge do you have?

Sources of external knowledge?

Each participant in the LMFDB brings on specific mathematical knowledge about the objects studied, which might not be available to others in the collaboration. The LMFDB has the concept of "knowls", which are encyclopedic bits of content integrated alongside the data, and editable collaboratively.

Can you point to implicit knowledge? Is it common knowledge?

There is a lot of implicit knowledge in the encodings chosen for the data (ad hoc formats and references), some of it is made explicit (for instance here). There is also a lot of implicit knowledge in the source code. There is little common knowledge across the collaboration, or at least there is a lot that is not common.

What would you gain if it was made explicit/machine actionable?

I (Paul) think the development process could be made more robust and efficient. The knowls currently serve as entry points for users and crucially also for onboarding future collaborators, as a stable basis for further collaboration. LMFDB could gain in productivity, robustness and ultimately utility if this process could be extended a bit further.

Have you gone in this direction? How did you represent the knowledge then?

The furthest the LMFDB has gone into the direction of formalising knowledge is in modularising as much as possible of the mathematical knowledge through knowls, creating an ad hoc ontology to classify them, and aligning it to the mathematical data objects that are presented. The LMFDB also tries to adhere to the concept of "one URL per object".

How do you collaborate on knowledge representation?

Edition of the knowls requires an account, which the LMFDB intends to offer to anyone. There is some versioning in place for knowls.

What software do you have?

The LMFDB is mostly written in Python, relies on Sage and Pari/GP as libraries. It uses the database MongoDB (and possibly also an SQL one), uses the web framework Flask, and the templating engine Jinja.

What custom software are you running?

In a way Sage is custom, since lots of LMFDB developers also contribute to Sage. Otherwise a whole lot of the logic is embedded in the website code.

In which language?

In the Flask framework.

How does it use the data and the knowledge?

Generally, a URL path will be associated to a Jinja template, requiring simultaneous fetching of pre-entered knowledge (knowls, Mongo DB), precomputed data (Mongo DB), and on-the-fly computation based on this precomputed data or existing functions implemented in some of the Computer Algebra Software already used.

How does your software act on represented knowledge?

As far as I know, it doesn't, except to display knowls.

Mixing (revisit?)

Which knowledge is implicit in the data you have?

Again, a lot of the data encoding is implicit in the data. For instance, [0,4,5,1] might represent the polynomial 4x+5x^2+x^3 or the polynomial x(x-4)(x-5)(x-1).

Which knowledge is implicit in the software you have?

When populating templates, some of the mathematical knowledge might be really entered through the code, by completing the template in different ways according to the calling class (example: elliptic curve L-functions are of degree 2).

Anything else?

Nope



On 14 December 2015 at 12:54, pdehaye <notifications@github.com> wrote:
 @JohnCremona <https://github.com/JohnCremona> : Let me know if you have
 something to add or clarify to the draft answers listed above. Thanks!
Thanks for making a good start on this.  I do have some comments, some of
which reflect rather recent changes and decisions made during the
just-finished semester at ICERM which included weekly LMFDB working
sessions.

About uploading of data: "This option is still there, but sees little
use."  This has never been a realistic option, and is not even visible
unless a user of the website is a developer with an account and is logged
in.  Perhaps best to say "This option has never been used seriously, and is
not currently supported."

"In general, proper referencing of data sources and documentation of its
quality is a struggle."   Progress has been made on these through a new
collection of "data quality" knowls, see
http://www.lmfdb.org/knowledge/?category=dq .  This only started within the
last few weeks but the intention is to have source / extent / quality /
reliability all documented for the main sections of the database by next
March's workshop.  As an example, see all elliptic curve pages such as
http://www.lmfdb.org/EllipticCurve/Q/  there is a "Learn more about"
section in th euppoe right which links to these knowls.

Under "How is [the data] changed" we could say more though it is not
uniform across the LMFDB.  In the best cases, the data is stored completely
separately fom the LMFDB's own (mongo) database, e.g. in my ecdata github
repository, under full revision control of text files;  and there are
scripts to populate the d.b. from that.

The process of documenting the data formats is ongoing, as has been driven
recently by the writing of the API by Harald Schilly -- all very new.

I don't know if it is relevant here but we are also accumulating a set of
bibliographic references and have already instuted a system for making
citations within knowls very easy.


# Sage

% 

Suggestions from Paul:
  - skim over sage databases (i.e. mention they exist, not more)
  - talk about different uses of category framework, including Florent's tricks of adding new axions to check consistency
  - talk about persistence/pickling of math objects as one point where semantics are implicit
## Overview at a high level of your system

  Give a 5 minute talk about the mathematics we need to grasp what you
  are trying to achieve with your system. This means introducing the
  concepts that are important, focusing on how they relate, rather
  than their definition. This is not concerned with questions of
  implementation of your system, yet.

- [SageMath](http://www.sagemath.org): General purpose computational (pure) mathematics software

- 300 contributors

- 1.5M lines of Python/Cython code

- 40k functions

- 4k classes

- hundreds of open source (math) software/libraries in the distribution

--

---
## What data do you have?

### A collection of (optional) databases:

- Usually coming from external software/databases

- Examples:

  - GAP databases
  - OEIS
  - John's database of elliptic curves
  - ...

---
### Pickling / Serialization

Objects can be converted to strings and reconstructed

- Applications:

  - Persistence
  - Sage databases
  - Exchange of data between Sage instances

- Format: Python's pickle protocol

  - Code to reconstruct the object + sanity checks
  - By default: pickling by class + plain data (no encapsulation)
  - Aiming for: pickling by construction (more semantic)


1. Structure
1. Format
1. How is it produced?
1. How is it changed?
1. How do you document it?

---
## What knowledge do you have?

Mathematical properties and theorems, algorithms, ...


## Two key points that conditioned the design

- There are only a handful of fundamental concepts:

  operations: *, +, ...

  axioms: associativity, commutativity, ...

  Richness in the combinations of them (e.g. Fields)

- Using an existing language and its object oriented features for
  modelling and method selection


### Sources of external knowledge?

Each Sage contributer brings on specific mathematical knowledge about
the objects studied, which might not be available to others in the
collaboration.

--

### Can you point to implicit knowledge?

- The algorithms rely heavily on the mathematical properties of
  the objects they manipulate.

- Sage uses the Object Oriented features of Python

  The properties of a Sage object are specified by its *class*:

  - what mathematical object does it represent?

  - how is it represented

- The class information is often of technical flavor, and complemented
  by additional information on its universe (parent, category)

--
- Sage strives to model mathematics closely:

  Not only matrices are instances of a specific classes and not plain
  list of lists

  But linear maps are instances of specific classes and not just
  represented by matrices

  ==> Reduced risk of calling a meaningless function

--

- The abstract algebraic properties of an object (e.g. being a group
  or a field) are modelled relatively explicitely:

  Objects know the names of their categories and axioms

  Meaning essentially implicit except, in the good cases, informally
  in the documentation and as testing methods

- The names of the operations are hardcoded

  ==> duplication: additive / multiplicative / lie magmas

  Morphisms by automatic renaming? Lacks static typing?

- Taming the exponential blow

  Size of the code linear in the number of methods

--
- It's not always defined explicitly which methods an object in a
  given category should implement.

  Methods/operations are documented, but their exact specifications of
  is not always completely defined/defined consistently accross the
  class hierarchy.

- Some theorems (e.g. wedderburn) are embedded in actionable form,
  but that information cannot be extracted / operated on

--
### Is it common knowledge?

The meaning of the relevant categories / axioms (e.g. ring,
associativity) is relatively well known by the users and developpers.

--
### What would you gain if it was made explicit/machine actionable?

- Dynamic generation of documentation that the user can navigate
- Sanity/correctness checks; proofs?
- Semantic handles to communicate with other systems
- Avoiding duplication (additive magmas / multiplicative magmas)?

### Have you gone in this direction? How did you represent the knowledge then?

- Categories / axioms were a first step :-)

### How do you collaborate on knowledge representation?

- Collaborative development of code / doc / tests in the Sage sources

---
## What software do you have?

### What custom software are you running?

- 1.5 M lines for the Sage library + all the rest

### In which language?

- Python/Cython + myriads of languages used by subsystems

### How does it use the data and the knowledge?

- As a fundation for its hierarchy of classes/categories

- Those are used for code factorization, documentation, and generic testing

--

### How does your software act on represented knowledge?

- Some computations in the lattices of categories:

  X is a division ring and X is a finite set

  ==> X is a finite field

---
## Mixing (revisit?)

### Which knowledge is implicit in the data you have?

### Which knowledge is implicit in the software you have?

- Formal definition of axioms

  That can be manipulated by the machine

- Formal specifications of methods

  That can be manipulated by the machine

1. Anything else?

Nope


# Gap

 https://github.com/OpenDreamKit/OpenDreamKit/issues/165

# MMT


 - codecs

 - http://opendreamkit.org/meetings/2016-01-25-DKS/report/

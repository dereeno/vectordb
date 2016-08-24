# Vector Database Homework

## Objectives

1. Examine the JSON dump of the Addgene DNA vector collection in the data
   folder and the web user interface on www.addgene.com. Design a data
   storage system to enable the following behaviors:
   - Find all vectors with a common attribute (ie. name)
   - Find all vectors where a child (nested) object has some attribute
   - Allow upload/import of the entire collection yet differentiate
     between records that don't conform to some schema (ie. incomplete,
     wrong cardinality)
   - Allow searches for records containing a particular DNA sequence
     (ie.'ATG') with up to some number of mismatches
   - Allow for the sequence(s) of records to be updated if mistakes are
     found without compromising integrity
   - Allow for new attributes to be added to existing records
     retroactively easily

2. Prepare a 30 min talk proposing your design from (1) for an audience of
   developers and subject matter experts. Some areas you might consider
   are:
   - Description of the logical data model
   - Design rational and key assumptions
   - Possible areas of high technical risk 
   - Performance limitations
   - Choice of implementation and technology stack
   - Implementation timeline
   - Maintainability or flexibility

3. Implement a proof-of-concept version of the system to illustrate some
   key aspect of its design. Focus on one or more areas of key technical
   uncertainty, novel aspects, or likely performance bottlenecks. 


## Background

Since the advent of DNA sequencing and cloning in the 1970s, numerous
databases of DNA molecules and their sequences have emerged. Common to all
of them is the difficulty of creating a structured or normalized
representation of a given DNA molecule whether it be a 30 base pair primer
or an entire genome. To this day domain experts debate whether such
a level of structure is even possible or if biological data is
intrinsically unstructured. Is NoSQL the solution? Bioinformaticians
report that 90% of their time is spent cleaning and normalizing data
rather than doing meaningful analysis and customers regularly cite high
data integrity as a key feature. This is an area of clear and immediate
unmet need.

This repository contains a JSON dump of the very popular Addgene
(www.addgene.org) DNA vector (plasmid) database. This catalog is searched
by thousands of scientists around the world every day yet it remains
difficult to find these vectors as there is no controlled vocabulary, no
automated annotation, minimal schema validation, and no agreed standards.
In many cases the full DNA sequence has not even been independently
verified. Despite this, Addgene's DNA vectors are used in large percentage
of non-profit research projects to introduce and move DNA sequences
between cells (and there much larger genomes) in the laboratory. Thus this
is an excellent representative sample of biotech data.


Biotech software has unusual usage patterns. Queries per second is MUCH
less important in this domain than query accuracy. Queries tend to be have
large result sets or be complex rather than frequent. Further once data is
"published" it is seldom updated and is largely read only. There is also
a long standing convention in paper scientific lab notebooks to never
erase data or records, even if wrong, but to strike out incorrect
information and write a correct alongside. The time and date when a record
was generated or last modified and the identity of the author is extremely
important and has been the subject of many multi-billion dollar disputes
over who was "first to invent" or "first to publish".


## Rules

1. Work must be your own. You may use any resource at your disposal
   including other people. You may ask questions.

2. You may use any language or technology for your solution, but your
   implementation must be portable an able to run on Ubuntu 14.04. You
   should include instructions on how to set up your solution and specify
   any dependencies. Internally we are most familiar Python and Postgresql
   and can deploy natively, to virtual machines or with Docker containers
   if needed.

3. Code quality, comments, documentation, test or profiler coverage, and
   showing your thought process count more than the number of features
   implemented.

4. The assignment is intended as a "weekend project" in scope. However it
   is untimed and you may take longer. Solutions will be assessed on
   a rolling basis.

5. You are not constrained to a single executable or process. You may use
   foreign data wrappers or otherwise delegate functionality to other
   processes.

6. It's not necessary to load the entire data set, but it would be a more
   accurate test of the system.

## Resources

- A live, searchable version of this data is available at www.addgene.com.
  Further this site contains a wealth of resources about DNA,
  biotechnology, and genomics.

- The Biopython library contains codes for working with DNA records and
  sequences. There are port of this library in most other languages.

- The European Bioinformatics Institute (EBI), Nation Center for
  Biotechnology Information (NCBI), and their Japanese colleagues operate
  freely available sequence databases. 

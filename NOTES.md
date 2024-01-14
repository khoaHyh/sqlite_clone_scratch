# Notes

### Part 1

Used ChatGPT to understand what happens to the query input when it goes to the front-end. I summarized ChatGPT's output
to help myself grasp the concepts learned.

* Front-end here refers to the user interface or application layer that enables users or other software to
  interact  with the SQLite database.
    * The output is SQLite VM bytecode that the back-end will take in as instructions.

Front-end consists of:

* **tokenizer** - responsible for breaking down input SQL query into sequence of tokens. The tokenizer scans the input character by character and identifies
  keywords, identifiers, literals, and other syntactic elements. It outputs a stream of tokens that the parser will use.
* **parser** - parser takes a stream of tokens and constructs a syntactic tree or parse tree. The parser enforces grammer rules of the SQL language. If the 
  query is syntactically correct, the parser generates a parse tree that represents the query's structure
* **code generator** - takes the parse tree and produces a set of instructions for the DB engine to
  follow in order to fulfill the query. The code generator transforms the parse tree into an intermediate presentation
  or machine code that can be executed by the DB engine. This involves optimizing the execution plan, considering factors
  such as indexes, joins, etc.

Back-end consists of:

* **virtual machine** - takes bytecode generated by the front-end as instructions. It can then perform operations on one or more tables or indexes, 
  each of which is stored in a data structure called a B-tree. The VM is essentially a big switch statement on the type of bytecode instruction.
* **B-tree** - known as a Balance Tree, is a data structure used to organize and store data. Each B-tree consists of many nodes. Each node is one 
  page in length. The B-tree can retrieve a page from disk or save it back to disk by issuing commands to the pager.
* **pager** - receives commands to read or write pages of data. It is responsible for reading/writing at appropriate offsets in the database file. 
  It also keeps a cache of recently-accessed pages in memory, and determines when those pages need to be written back to disk.
* **os interface** - is the layer that differs depending on which operating system sqlite was compiled for. In this tutorial, I'm not going to 
  support multiple platforms.
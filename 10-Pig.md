# Pig

* Pig latin (a language to express data flows)
* Execution environment: local or on hadoop cluster

Pig is for explore large datasets and is extensible. It cannot explore subsets.

## Hadoop mode

Pig translates queries into MapReduce jobs. The pig.properties must have:

	fs.default.name=hdfs://localhost/
	mapred.job.tracker=localhost:8021

## Running Pig Programs

* **Script**: A file with commands. PigPen is an Eclipse Plugin
* **Grunt**: Interactive shell
* **Embedded**: From Java using **PigServer** class

## Some example commands

* **LOAD (sample.txt) as (year:chararray, temperature int);** loads a file delimited by tabs
* **DUMP var;** Shows the contents of a var
* **DESCRIBE var;** Shows info about a var
* **FILTER records BY temperature != 9999** Filters a loaded file
* **GROUP filtered_records BY year;** Groups the contents using a column
* **FOREACH grouped_records GENERATE group;** Foreach process every row to to generate a derived set of rows with the fields of the GENERATE clause.
* **ILLUSTRATE var;** Shows pretty info of a var.

TODO insert the table of the page 398


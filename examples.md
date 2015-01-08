---
layout: page
title: Examples
permalink: /examples/
---


### Example \#1

#### CSV data

The following lines are part of a CSV file (`TechCrunchcontinentalUSA.csv`) snapshot that contains information about companies.

{% highlight bash %}
permalink,company,numEmps,category,city,state,fundedDate,raisedAmt,raisedCurrency,round
lifelock,LifeLock,,web,Tempe,AZ,1-May-07,6850000,USD,http://example.com/b
lifelock,LifeLock,,web,Tempe,AZ,1-Oct-06,6000000,USD,<http://example.com/a>
lifelock,LifeLock,,web,Tempe,AZ,1-Jan-08,25000000,USD,c
mycityfaces,MyCityFaces,7,web,Scottsdale,AZ,1-Jan-08,50000,USD,seed
flypaper,Flypaper,,web,Phoenix,AZ,1-Feb-08,3000000,USD,a
infusionsoft,Infusionsoft,105,software,Gilbert,AZ,1-Oct-07,9000000,USD,a
gauto,gAuto,4,web,Scottsdale,AZ,1-Jan-08,250000,USD,seed
chosenlist-com,ChosenList.com,5,web,Scottsdale,AZ,1-Oct-06,140000,USD,seed
chosenlist-com,ChosenList.com,5,web,Scottsdale,AZ,25-Jan-08,233750,USD,angel
digg,Digg,60,web,San Francisco,CA,1-Dec-06,8500000,USD,b
digg,Digg,60,web,San Francisco,CA,1-Oct-05,2800000,USD,a
facebook,Facebook,450,web,Palo Alto,CA,1-Sep-04,500000,USD,angel
facebook,Facebook,450,web,Palo Alto,CA,1-May-05,12700000,USD,a
facebook,Facebook,450,web,Palo Alto,CA,1-Apr-06,27500000,USD,b
facebook,Facebook,450,web,Palo Alto,CA,1-Oct-07,300000000,USD,c
facebook,Facebook,450,web,Palo Alto,CA,1-Mar-08,40000000,USD,c
facebook,Facebook,450,web,Palo Alto,CA,15-Jan-08,15000000,USD,c
facebook,Facebook,450,web,Palo Alto,CA,1-May-08,100000000,USD,debt_round
...
{% endhighlight %}

#### Tarql mapping

We could define a mapping to convert the previous CSV file into RDF triples using the following mapping:

{% highlight bash %}
PREFIX ex: <http://ex.org/a#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

CONSTRUCT {
  ?URI a ex:Organization;
    ex:permalink ?permalink;
    ex:name ?company;
    ex:employees ?numEmployees;
    ex:category ?category;
    ex:city ?city;
    ex:state ?state;
    ex:fundationDate ?fundedDate;
    ex:raisedAmt ?amount;
    ex:raisedCurrency ?raisedCurrency;
    ex:round ?round;
} 
FROM <file:TechCrunchcontinentalUSA.csv> 
WHERE {
  BIND (URI(CONCAT('http://ex.org/companies/', ?permalink)) AS ?URI)
  BIND (xsd:integer(?numEmps) AS ?numEmployees)
  BIND (xsd:decimal(?raisedAmt) AS ?amount)
}
{% endhighlight %}

In the previous mapping we have indicated the following:

* how each column will be mapped with a predicate, with respect to the main resource (?URI)
* which file are we trying to convert (`file:TechCrunchcontinentalUSA.csv`)
* how we can apply datatypes to some of the variables (BIND clauses)

#### Result

Executing Tarql with the previous mapping:

{% highlight bash %}
tarql/target/appassembler$ sh bin/tarql --ntriples ../../test/sample-2.sparql ../../test/TechCrunchcontinentalUSA.csv
{% endhighlight %}

We do get the following RDF in N-Triples format.

{% highlight bash %}
<http://ex.org/companies/lifelock> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://ex.org/a#Organization> .
<http://ex.org/companies/lifelock> <http://ex.org/a#permalink> "lifelock" .
<http://ex.org/companies/lifelock> <http://ex.org/a#name> "LifeLock" .
<http://ex.org/companies/lifelock> <http://ex.org/a#category> "web" .
<http://ex.org/companies/lifelock> <http://ex.org/a#city> "Tempe" .
<http://ex.org/companies/lifelock> <http://ex.org/a#state> "AZ" .
<http://ex.org/companies/lifelock> <http://ex.org/a#fundationDate> "1-May-07" .
<http://ex.org/companies/lifelock> <http://ex.org/a#raisedAmt> "6850000"^^<http://www.w3.org/2001/XMLSchema#decimal> .
<http://ex.org/companies/lifelock> <http://ex.org/a#raisedCurrency> "USD" .
<http://ex.org/companies/lifelock> <http://ex.org/a#round> <http://example.com/b> .
<http://ex.org/companies/lifelock> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://ex.org/a#Organization> .
<http://ex.org/companies/lifelock> <http://ex.org/a#permalink> "lifelock" .
<http://ex.org/companies/lifelock> <http://ex.org/a#name> "LifeLock" .
<http://ex.org/companies/lifelock> <http://ex.org/a#category> "web" .
<http://ex.org/companies/lifelock> <http://ex.org/a#city> "Tempe" .
<http://ex.org/companies/lifelock> <http://ex.org/a#state> "AZ" .
<http://ex.org/companies/lifelock> <http://ex.org/a#fundationDate> "1-Oct-06" .
<http://ex.org/companies/lifelock> <http://ex.org/a#raisedAmt> "6000000"^^<http://www.w3.org/2001/XMLSchema#decimal> .
<http://ex.org/companies/lifelock> <http://ex.org/a#raisedCurrency> "USD" .
<http://ex.org/companies/lifelock> <http://ex.org/a#round> <http://example.com/> .
<http://ex.org/companies/lifelock> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://ex.org/a#Organization> .
<http://ex.org/companies/lifelock> <http://ex.org/a#permalink> "lifelock" .
<http://ex.org/companies/lifelock> <http://ex.org/a#name> "LifeLock" .
<http://ex.org/companies/lifelock> <http://ex.org/a#category> "web" .
<http://ex.org/companies/lifelock> <http://ex.org/a#city> "Tempe" .
<http://ex.org/companies/lifelock> <http://ex.org/a#state> "AZ" .
<http://ex.org/companies/lifelock> <http://ex.org/a#fundationDate> "1-Jan-08" .
<http://ex.org/companies/lifelock> <http://ex.org/a#raisedAmt> "25000000"^^<http://www.w3.org/2001/XMLSchema#decimal> .
<http://ex.org/companies/lifelock> <http://ex.org/a#raisedCurrency> "USD" .
<http://ex.org/companies/lifelock> <http://ex.org/a#round> "c" .
<http://ex.org/companies/mycityfaces> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://ex.org/a#Organization> .
<http://ex.org/companies/mycityfaces> <http://ex.org/a#permalink> "mycityfaces" .
<http://ex.org/companies/mycityfaces> <http://ex.org/a#name> "MyCityFaces" .
<http://ex.org/companies/mycityfaces> <http://ex.org/a#employees> "7"^^<http://www.w3.org/2001/XMLSchema#integer> .
<http://ex.org/companies/mycityfaces> <http://ex.org/a#category> "web" .
<http://ex.org/companies/mycityfaces> <http://ex.org/a#city> "Scottsdale" .
<http://ex.org/companies/mycityfaces> <http://ex.org/a#state> "AZ" .
<http://ex.org/companies/mycityfaces> <http://ex.org/a#fundationDate> "1-Jan-08" .
<http://ex.org/companies/mycityfaces> <http://ex.org/a#raisedAmt> "50000"^^<http://www.w3.org/2001/XMLSchema#decimal> .
<http://ex.org/companies/mycityfaces> <http://ex.org/a#raisedCurrency> "USD" .
<http://ex.org/companies/mycityfaces> <http://ex.org/a#round> "seed" .
...
{% endhighlight %}

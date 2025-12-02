---
tags:
  - copyright
  - opendata
  - webcrawl
title: "milieau.02 requirements and evaluation"
---

I'll segment the two logical parts of this project for this requirements file, because they are separate entities, and only come together near the end. I will also split the requirements into functional and non-functional sets to keep a clear vision of the different aspects. Within those steps I'll evaluate verbally how critical each requirement is.

### Crawler

#### Functional

The program shall:
- browse and collect data from specified websites.
- only collect specified data, only that which is necessary.
- fit the collected data to a specified machine readable format, which can be used with the milieau dataset.
- be used through CLI.
- be only run as a one time process or be timed to run at specified intervals with cron.
- crosscheck for duplicates in the collected dataset and retain only one.
- validate retrieved data.

#### Non-functional

- Python as programming language.
- Code shall use OOP.
- The code shall be tested with unit testing.
- Version control with Git.
- Process documentation in MD and further published to blog.
- Code documented in Doxygen format.
-  Style and naming conventions of PEP-8 followed.
- Ubuntu 24.04 and VS Code used as development OS and IDE.

#### Evaluation

The functional requirements should all be achievable in implementation, as they are general and related closely to the primary objectives of the project. The first three points are quite vague and the implementation specifics will need to be set in the future. I use "specified" as a placeholder for something that needs to be specified. 

The OOP principles should come into play when specifying the websites. I want to have a generic class for the crawler which is inherited in subclasses for each website I want to crawl for data. I want to keep the interface to the websites as minimal as possible as a principle as well as keeping the website specific code outside of Github. I feel that offering website specific calls goes against my ethics. I also want to practice planning and implementing a somewhat rigid design pattern, so that I don't have to rewrite code structure in the future.

For the same objective I want to stress PEP-8 style and naming conventions, so that I don't have to think about how to name code objects infividually but have a concrete structure and guidelines to naming. I feel that I've learned a clear style / structure already, so that doesn't have to be stressed that heavily.

The machine radable data format I'll choose will most likely either be CSV or JSON. I personally enjoy using CSV more, so that might be what I choose to use. Nevertheless, I will explore JSON more and try to model the necessary fields I need to both JSON and CSV and decide on which to use.

Unit testing is also possibly not necessary for a project of this size (small) and one won't be developed to have more dependencies and features in the future. I want unit testing, because in my previous (embedded) project I couldn't implement it when it would've accelerated debugging once set up. I haven't used unit testing in Python before.

CLI will be used so that I have to think about UI less. It will be formatted with a program call and arguments that specify program behaviour, like which website is being crawled and where the result should be placed.

Data validation should be as follows: The program warns the user of empty fields and non standard datatypes so they can be addressed by the user.

### Analysis

- The primary tools used shall be Python and Excel
- The datasets are not huge so it is possible that nothing conclusive can be said.
- I will plot the crawled data onto the milieau sectors using Openstreetmaps
- The crawled data should have the unique milieau sectors as a field.
	- The uniqueness is important because milieau sectors can be split over independent sections of the city, where the explanation of price can be formed using other figures, such as closeness to city center.
- The analysis is supposed to only find out if there is any correlation and further what is the causation of property prices and environment using the available information from the public property listings.
	- the prices should be normalized using a combination of variables from the crawled information so that property values can be compared to each other hopefully more accurately.
	- It should cut out any noise that is introduced by differing conditions for the apartments, for the apartment complex, for size, age etc. 

#### Evaluation

This section has been more out of order than the pure programming part because I don't know as much about statistical analysis as I do programming. I intend on learning about regression models once I get there so that I can normalize the features of apartments to compare prices better. There might even be studies on what features affects apartment prices, which I might be able to use here. The goal is to make educated and reasoned guesses for the model and analyze in that light, not stray too far from the uncertainty of my methods.

As for the uncertainty factors:
1. Because a program has retrieved the information about the properties nuances of how a price is set might be lost.
2. The websites I will use might not present an accurate spread of apartments in any given area.
3. Because the crawled data consists only of active property listings it 
	1. doesn't take into consideration the historical development of values.
	2. might be too limited in size.
	3. only shows what properties are listed for, not their final sale values.
# Introduction to the Unix Shell for Data Science

*This document proposes a new format for DataCamp course outlines
and a new process for developing them,
based on both Wiggins & McTighe's *[Understanding by Design][ubd]*
and [Software Carpentry's experience][teaching].
Feedback would be greatly appreciated.*

## Step 0: Learner Profiles

*Terms like "beginner" and "expert" mean different things to different people,
so these profiles make the course's intended audience concrete.
Profiles typically have [five parts][learner-profiles]:
the learner's general background,
what they already know,
what they think they want to do,
any special needs they might have,
and how the course will help them.
DataCamp will have a handful of stock profiles that define the first four points;
particular course outlines will reference these and add the fifth.*

*Output: brief descriptions of intended audience.*

(Images courtesy of [RoboHash][robohash].)

**Jasmine**

![Jasmine](img/jasmine.png)

1. Jasmine, 28, did a commerce degree at the University of North Carolina,
   and then an MBA at Georgia State.
   In the three years since completing it,
   she has been doing health insurance policy research for an underwriter.

2. Jasmine did a stats class as an undergrad
   and another in grad school (which covered almost exactly the same material).
   She uses Excel every day,
   and is comfortable doing simple operations in SAS.

3. Jasmine would like to start teaching data analysis at her alma mater.
   Her boss has given her two afternoons a week of work release to do this,
   and she wants to level up her statistical and computing skills
   as quickly as she can.

4. Jasmine is partially deaf,
   and strongly prefers written and visual material to spoken material.

5. This course will give Jasmine a basic understanding of the Unix shell
   so that she can help her students solve the problems they encounter
   using the university's systems in their statistics courses.

**Thanh**

![Thanh](img/thanh.png)

1. Thanh, 35, has an undergraduate degree in psychology with a minor in statistics.
   He now works for the Quebec Ministry of Education,
   where he helps administer programs for children with learning disabilities.

2. Thanh uses classical statistical methods every day.
   He taught himself the basics of R,
   and then used DataCamp's courses to learn more.

3. Thanh is about to join a consortium that is analyzing different approaches to special education.
   As part of this,
   he wants to start building tools that other consortium members can use.

4. Thanh is fluent in Vietnamese and French,
   but only has high school English
   (supplemented by a solid technical vocabulary).

5. This course will show Thanh how to build command-line tools
   and use remote computing resources (such as clusters),
   and is a step toward building [robust software][robust-software].

## Step 1: Concept Map

*This is a brainstorming stage to determine what we want learners to know at the end of the course.
Its concrete output is usually a [concept map][concept-map] showing the main ideas and their relationships,
but in some cases it may be more helpful to represent the goal as a [decision tree][abela-chart]
or some other graphical form.*

*Output: graphical representation of learner's final mental model.*

![Basic Unix Concepts](img/unix.png)

*Notes:*

1. *It's tempting to write learning objectives at this point.
   Resist!
   Step 4 will almost certainly result in material being cut.*

2. *If this is your first time creating a concept map, 
   you may struggle with this step.
   Have no fear—we're here to help!*

## Step 2: Summative Assessment

*The best way to make the goal of a course concrete is
to present examples of what learners will be able to do at its end.
This is directly analogous to [test-driven development][tdd]:
rather than working forward from a (probably ambiguous) set of learning objectives,
designers work backward from concrete examples of where their learners are going.*

*Output: 2-3 exercises that use all of the skills the learner is to develop.*

### Summative Exercise 1: Shell Scripts

You have several dozen data files, each of which is formatted like this:

```
2013-11-05,deer,5
2013-11-05,rabbit,22
2013-11-05,raccoon,7
2013-11-06,rabbit,19
2013-11-06,deer,2
2013-11-06,fox,1
2013-11-07,rabbit,18
2013-11-07,bear,1
```

Write a shell script called `unique.sh`
that takes any number of filenames as command-line parameters
and prints the names of the species found in each file
in alphabetical order.
Each file is processed separately.

> **Solution**
>
> ```
> #!/usr/bin/env bash
> 
> # Find unique species in CSV files where species is the second data
> # field.  This script accepts any number of filenames as arguments
> # and processes each separately.
> 
> for file in $@ 
> do
>   echo $file
>   cut -d , -f 2 $file | sort | uniq
> done
> ```

### Summative Exercise 2: Wildcards

The directory `./data` contains four CSV files and three shell scripts:

```
$ ls *.csv
autumn.csv	spring.csv	summer.csv	winter.csv

$ ls *.sh
first.sh	second.sh	third.sh
```

If the shell scripts contain the commands shown below,
what will be the output of:

1. `./first.sh *.*`
2. `./second.sh *.*`
3. `./third.sh *.*`

```
# first.sh
echo *.*
```

```
# second.sh
for filename in $1 $2 $3
do
  cat $filename
done
```

```
# third.sh
echo $@.csv
```

> **Solution**
>
> `first.sh` will display:
>
> ```
> autumn.csv first.sh second.sh spring.csv summer.csv third.sh winter.csv
> ```
>
> because `*.*` inside the script matches all two-part filenames,
> and the command-line arguments are ignored.
>
> `second.sh` will display the contents of `autumn.csv`, `spring.csv`, and `summer.csv`.
>
> `third.sh` will display:
>
> ```
> autumn.csv spring.csv summer.csv winter.csv.csv
> ```
>
> Note the double `.csv` at the end:
> the expression `$@` expands to the names of the command-line arguments,
> and then the explicit `.csv` in the script is tacked on.

*Notes:*

1. *These summative assessments will normally be included in the course
   as its final exercises.*

2. *If we find this approach productive,
   we may eventually stitch these concept maps together
   to create something like Kamran Ahmed's [developer roadmap][developer-roadmap].

## Step 3: Formative Assessments

*Formative assessments are exercises done while learning is taking place,
rather than at the end to determine whether it has.
Formative assessments serve two purposes:
to tell the learner and the instructor if learners are making progress
(or conversely, what they still need to work on),
and to give learners a chance to exercise the skills and knowledge
they will need in the summative assessment.*

*In order to create formative assessments,
you'll work backward from the summative assessment written in Step 2.
Make a point-form list of the skills needed to solve the summative assessment
and create a formative assessment for each,
then itemize the extra skills those exercises depend on,
and repeat until only prerequisite skills are left.*

*Output: a set of formative assessments that exercise all the skills you intend to teach.
These will help communicate the concrete goals of the course to others,
and help you uncover dependencies you didn't realize you had.*

### Formative Exercise: Shell Scripts

Fill in the blanks in the shell script `dates.sh`
to select unique dates from the files
whose names are given as the script's command-line arguments.

Uses:
- command-line arguments
- pipes
- wildcards
- `cut`, `sort`, `uniq`
- `#!`

### Formative Exercise: Wildcards

Suppose you want to delete the output files in the `results` directory
and any raw files that have mistakenly been copied into the current directory
without deleting anything else.
The raw files' names end in `.dat` and the processed files' names end in `.out`.
Which of the following would do what you want?

1. `rm results/* .raw`
2. `rm results/*.out ~/*.raw`
3. `rm *.dat ?/*.out`
4. `rm ./*.dat results/*.out`

Uses:
- paths
- `*` and `?` wildcards

### Formative Exercise: Tracing Pipes and Redirection

A file called `dental.csv` contains the following data:

```
2017-05-05,incisor
2017-05-05,bicuspid
2017-05-05,molar
2017-05-06,bicuspid
2017-05-06,incisor
2017-05-06,premolar
2017-05-07,bicuspid
2017-05-07,crown
```

What text passes through each of the pipes and the final redirect in the pipeline below?

```
$ cat dental.csv | head -n 5 | tail -n 3 | sort -t , -k 2 > final.txt
```

Uses:
- `cat`, `head`, `tail`, `sort`
- pipes
- redirection
- command flags

### Formative Exercise: Selecting Data by Value

A file called `dental.csv` contains 2000 lines formatted as follows:

```
2017,incisor
2017,bicuspid
2016,bicuspid
2016,premolar
2015,bicuspid
2015,crown
...
2000,bicuspid
2000,premolar
```

Write a command that selects *only* the data from the years 2000, 2005, and 2010.

Uses:
- `grep` (with fixed text, not regualr expressions)

### Formative Exercise: Manipulating Files and Directories

What is the output of the final `ls` command in the sequence shown below?

```
$ pwd
/Users/jasmine/data

$ ls
mortality.dat

$ mkdir old
$ mv mortality.dat old
$ cp old/mortality.dat ../mortality-saved.dat
$ ls
```

1. `mortality-saved.dat old`
2. `old`
3. `mortality.dat old`
4. `mortality-saved.dat`

Uses:
- `pwd`, `ls`, `cp`, `mv`, `mkdir`
- paths
- the special path `..`

### Formative Exercise: The Shell vs. GUIs

What is the relationship between the shell
and the graphical file explorer that most people use?

1. The file explorer lets you view and edit files, while the shell lets you run programs.
2. The file explorer is built on top of the shell.
3. The shell is part of the operating system, while the file explorer is separate.
4. They are both interfaces for issuing commands to the operating system.

Uses:
- the difference between an interface to an OS and the OS itself
- the idea of a filesystem

## Step 4: Course Outline

*In this stage,
formative assessments are put in an order that respects their dependencies.
This is the point at which you'll discover all the dependencies you forgot to list earlier.
You'll then create a point-form outline of chapters and lessons:
each chapter has a title and 3-5 lessons,
and each lesson has a handful of keywords describing what it will cover.*

*Output: an instructional sequence.*

The formative assessments in Step 3 are already in reverse order.
The chapter and lesson outline is:

1. Manipulating Files and Directories
   1. What a shell is; how it compares to a graphical interface.
   2. `whoami`; `pwd`; `ls`; files vs. directories
   3. `cp`; `mv`; `rm`
   4. The special paths `.` and `..`
   5. `cat`; editing text files with tools like `nano`
   6. `mkdir`; `rmdir`
2. Manipulating Data
   1. `head`; `tail`; command-line flags
   2. `man`
   3. `cut`
   4. `history`; `!number` and `!command`
   4. `grep`; single-quoting arguments to protect special characters
   5. `uniq`; `sort`
3. Combining Tools
   1. Redirection with `>`
   2. Piping with `|`
   3. Using the `*` and `?` wildcards
4. Automating Repeated Tasks
   1. Storing commands in files; running files with `bash script.sh`
   2. Permissions; `ls -l`; changing permissions; using `!#`
   3. Using positional arguments `$1`, `$2`, etc.
   4. Using `$@`
   5. Teaser for the next course in the sequence (shell loops and SSH)

## Step 5: Course Overview

*You're now ready to write the course's public interface:
its learning objectives,
a short blurb for the course catalog,
and its prerequisites.
(Doing this earlier often wastes effort,
since material may be added or cut in Step 4.)*

*Output: learning objectives, course overview, and prerequisites.*

**Course Description**

The Unix command line has survived and thrived for almost fifty years
because it lets people to do complex things with just a few keystrokes.
Sometimes called "the duct tape of programming",
it helps users combine existing programs in new ways,
automate repetitive tasks,
and run programs on clusters and clouds
that may be halfway around the world.
This course will introduce its key elements
and show you how to use them efficiently.

> **Writing Good Learning Objectives**
>
> To write a good learning objective:
>
> 1. Identify the *main noun* (the thing you want learners to master).
> 2. Identify the *level of understanding* you want (discussed below).
> 3. Select an *observable verb*.
>    "Learner will understand X" isn't observable (at least, not until telepathy is productized),
>    but "learner will describe key points in the development of X" is.
>
> The most widely used classification of levels of understanding is [Bloom's Taxonomy][bloom].
> Its six levels and associated verbs are:
>
> 1. Knowledge: recalling learned information
>    (name, define, recall).
> 2. Comprehension: explaining the meaning of information
>    (restate, locate, explain, recognize).
> 3. Application: applying what one knows to novel, concrete situations
>    (apply, demonstrate, use).
> 4. Analysis: breaking down a whole into its component parts
>    and explaining how each part contributes to the whole
>    (differentiate, criticize, compare).
> 5. Synthesis: assembling components to form a new and integrated whole
>    (design, construct, organize).
> 6. Evaluation: using evidence to make judgments about the relative merits of ideas and materials
>    (choose, rate, select).

**Learning Objectives**

- Explain the similarities and differences between the Unix shell and graphical user interfaces.
- Use core Unix commands to create, rename, and remove files and directories.
- Explain what files and directories are.
- Match files and directories to relative and absolute paths.
- Use core data manipulation commands to filter and sort textual data by position and value.
- Find and interpret help.
- Predict the paths matched by wildcards and specify wildcards to match sets of paths.
- Combine programs using pipes to process large data sets.
- Write shell scripts to re-run command pipes with a varying number of command-line arguments.

**Prerequisites**

None.

## Conclusion

Thirty years ago,
[Parnas and Clements][parnas-clements] wrote:

> Many have sought a software design process that allows a program to be derived systematically
> from a precise statement of requirements.
> It is proposed that,
> although designing a real product in that way will not be successful,
> it is possible to produce documentation that makes it appear that the software was designed by such a process.

The same is true of courses:
this process is described as a one-way flow,
but in practice,
you will loop back repeatedly
as each stage informs you of something you overlooked.
Similarly,
you may add, move, or remove some specific lesson items after you begin writing exercises
(though we must approve any signficant structural changes to the course).

[abela-chart]: http://extremepresentation.typepad.com/.shared/image.html?/photos/uncategorized/choosing_a_good_chart.jpg
[bloom]: https://en.wikipedia.org/wiki/Bloom's_taxonomy
[concept-map]: http://third-bit.com/teaching/memory.html#concept-maps
[developer-roadmap]: https://github.com/kamranahmedse/developer-roadmap
[learner-profiles]: http://third-bit.com/teaching/lessons.html#learner-profiles
[parnas-clements]: http://ieeexplore.ieee.org/document/6312940/
[robohash]: http://robohash.org
[robust-software]: http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1005412
[tdd]: https://en.wikipedia.org/wiki/Test-driven_development
[teaching]: http://third-bit.com/teaching/
[ubd]: https://www.amazon.com/Understanding-Design-Grant-Wiggins/dp/1416600353/

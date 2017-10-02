# Designing DataCamp Courses

<em>

Designing a good course is as hard as designing good software.
To help you,
this document describes a process based on evidence-based teaching practices:

- It lays out a structured design process that helps you figure out
  what to think about in what order to design courses more quickly.
- It provides check-in points at which you and your Curriculum Lead (CL) can re-scope or redirect effort.
- The end product specifies deliverables clearly enough for you to be able to finish development without major surprises.
- Everything from Step 2 onward goes into your final course, so there is no wasted effort.
- Getting you to work through some sample exercises early gives us a chance to make sure
  that we can support all of the things you will want your students to do.

The steps are laid out in a particular order,
but the process itself is iterative:
you will frequently go back to revise earlier work
as you learn something from your answer to a later question
or realize that your initial plan isn't going to play out the way you first thought.

We use the design of our introduction to the Unix shell for data scientists as a running example;
please use [this Markdown template](template.md) as a starting point for designing your own courses.
For more information,
please see [How to create a DataCamp course][datacamp-how]
and [the teaching documentation][datacamp-teach].

## Terminology and Structure

- A **course** is a self-contained module with its own top-level entry in our catalog,
  its own GitHub repository,
  etc.
- A **chapter** is a major section of a course.
- Chapters are made up of **lessons**,
  each of which consists of a short video and a handful of **exercises**.

A course typically has about the same amount of content as a half-day conference workshop,
and contains 44-60 exercises (including videos) and 4-5 chapters.
A typical breakdown is:

- Chapter 1: 8-12 exercises
- Chapter 2: 10-16 exercises
- Chapter 3: 10-16 exercises
- Chapter 4: 10-16 exercises
- Chapter 5 (optional): 10-16 exercises

Each chapter begins with a video and videos are separated by 2-4 interactive exercises

</em>

<!-- -------------------------------------------------------------------------------- -->

## Step 1: Brainstorming

<em>

The first step is to throw together some rough ideas
so that you and your CL can make sure your thoughts about the course are aligned.
One way to do this is to write some point-form answers to the following questions:

1. *What problem(s) will student learn how to solve?*
   Examples include "how to draw plots using `ggplot2`",
   "how to run a random forest model",
   or "how to forecast the demand for a product".

2. *What techniques or concepts will students learn?*
   Examples include "combining plot elements using `+`",
   "the split-train-model-predict modeling workflow",
   or "rolling back Git commits".

3. *What technologies, packages, or functions will students use?*
   Examples include "`ggplot2` for drawing plots",
   "`experiment` for experimental design (but not sure whether to use `pwr` or `PwrGSD` for sample size calcs)",
   or "TBD: something for map-reduce computations".
   (It's OK at this stage to have placeholders.)

4. *What terms or jargon will you define?*
   Examples include "boosting versus bagging",
   "block/factorial/sequential designs",
   or "forecasting versus prediction".

5. *What analogies will you use to explain concepts?*
   Examples include "ggplots are like Lego for graphics"
   or "seasonality and trends are like revolution and evolution".
   (See [Gelman & Nolan][teaching-statistics] for more ideas here.)

6. *What heuristics will help students understand things?*
   Examples include "draw a simple plot then add elements one by one",
   "split the dataset into 70% training, 30% testing",
   or "don't use Holt-Winters if your demand spikes on holidays".

7. *What mistakes or misconceptions do you expect?*
   Examples include "changing colors works differently if the color argument is inside an aesthetic or not",
   "overfitting models to the data",
   and "floating point numbers behave like real numbers".

8. *What datasets will you use?*
   Examples include "anything but the diamonds and mtcars datasets",
   "something from the [UCI Archive][uci-archive]",
   or "TBD: WHO infectious disease data".

You may not need to answer every question for every course,
and you will often have questions or issues we haven't suggested,
but couple of hours of thinking at this stage can save days of rework later on.

Output: a rough scope for the course that you have agreed with your CL.

</em>

1. What problem(s) will student learn how to solve?
   - How to combine existing/legacy tools.
   - How to make analyses reproducible.
2. What techniques or concepts will students learn?
   - History.
   - Pipes.
   - Shell scripts.
3. What technologies, packages, or functions will students use?
   - Bash shell.
   - Basic Unix commands (`cd`, `ls`).
   - Basic data manipulation commands (`head`, `cut`, `grep`).
4. What terms or jargon will you define?
   - Filesystem.
   - Redirection.
   - Pipe.
   - Wildcard.
5. What analogies will you use to explain concepts?
   - Command-line pipeline is like chemistry pipeline.
   - Shell scripts are like snippets of command history.
6. What heuristics will help students understand things?
   - Use filenames that are easy to match with tab completion and wildcards.
   - Build pipelines step by step.
7. What mistakes or misconceptions do you expect?
   - The shell shows the same files and folders as the GUI interface they're used to.
   - Definition vs. use of variables (especially loop variables).
8. What datasets will you use?
   - Dental records (reduced to region, date, and tooth).

<!-- -------------------------------------------------------------------------------- -->

## Step 2: Who is this course for?

<em>

Terms like "beginner" and "expert" mean different things to different people,
and many factors besides pre-existing knowledge influence who a course is suitable for.
The second step in designing a course is therefore to make clear who it is intended to help and how.
To help you do this,
we have created [student profiles][profile-site] for typical DataCamp students.
Each profile has [four constant parts][learner-profiles]:
the person's general background,
what they already know,
what they think they want to do,
and any special needs they might have.

Once you are done brainstorming,
you should go through the profiles we have provided
and identify which of these students it will help and how.
While doing this,
you may want to add some notes about what you expect from particular students,
or even create another profile of your own if you feel that
the ones we have provided don't capture your intended audience.

Output: brief summaries of who your course will help and how.

Note: the [student profiles][profile-site] are representative abstractions of our actual and aspirational user community,
and will be updated as we gather more data about who is using our courses.
Please do not copy the profiles into your course design;
instead,
link to them and comment on how the course relates to them.

</em>

- [Jasmine](https://github.com/datacamp/learner-profiles#jasmine):
  This course will give Jasmine a basic understanding of the Unix shell
  so that she can help her students solve the problems they encounter
  using the university's systems in their statistics courses.

- [Thanh](https://github.com/datacamp/learner-profiles#thanh):
  We assume that Thanh can already use basic commands like `cd` and `ls`,
  and knows how to create pipelines.
  This course will show him how to build shell scripts
  and use remote computing resources (such as clusters).

- [Yngve](https://github.com/datacamp/learner-profiles#yngve):
  Yngve uses all of the tools and concepts that this course introduces on a daily basis,
  so he won't be interested in taking it.

<!-- -------------------------------------------------------------------------------- -->

## Step 3: How far will this course get its students?

<em>

The best way to make the goal of a course concrete is
to write one or two exercises that test what students will be able to do at its end.
This is directly analogous to [test-driven development][tdd]:
rather than working forward from a (probably ambiguous) set of learning objectives,
designers work backward from concrete examples of where their students are going.
(Wrapping-up exercises of this kind are technically called *summative assessments*.)

Output: 1-2 exercises that use most or all of the skills the student is to develop.

Note: these will normally be included toward the end of the course.
Be sure to include solutions with example code
so that the scope of the exercise is unambiguous.

</em>

You have several dozen data files, each of which is formatted like this:

```
2013-11-05,deer,5
2013-11-05,rabbit,22
2013-11-05,raccoon,7
2013-11-06,rabbit,19
```

1. Write a shell script called `unique.sh`
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

2. With one command,
   use `unique.sh` to find the unique species
   in all of the `.csv` files in the `~/archive` and `~/new` directories.
   Use wildcards to specify the names of the files to be processed;
   do *not* include the `.txt` or `.bak` files in those directories.

> **Solution**
>
> ```
> unique.sh ~/archive/*.csv ~/new/*.csv
> ```

<!-- -------------------------------------------------------------------------------- -->

## Step 4: What will the student do along the way?

<em>

*Formative assessments* are exercises done while learning is taking place,
rather than at the end to determine whether it has.
Formative assessments serve two purposes:
to tell the student and the instructor if students are making progress
(or conversely, what they still need to work on),
and to give students a chance to exercise the skills and knowledge
they will need in the summative assessment.

To create formative assessments,
work backward from the summative assessments written in Step 3.
Make a point-form list of the skills needed to solve the summative assessments
and create a formative assessment for each,
then itemize the extra skills those exercises depend on,
and repeat until every concept and connection in the concept map (Step 3) is covered.

Output: 5-10 exercises that use the skills you intend to teach.
These will help communicate the concrete goals of the course to others,
and help you uncover dependencies you didn't realize you had.

Notes:

- These exercises will normally be included in the finished course.
- They are **not** all of its exercises,
  but rather milestones along the way (typically 1-2 per chapter).
- Do not worry about their order;
  you will do that in the next step.
- As with the summative assessments,
  be sure to include solutions with example code
  so that the scope of each exercise is unambiguous.

</em>

### Manipulating Files and Directories

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

### Wildcards

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

### Tracing Pipes and Redirection

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

### Selecting Data by Value

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

### Shell Scripts

Fill in the blanks in the shell script `dates.sh`
to select unique dates from the files
whose names are given as the script's command-line arguments.

Uses:
- command-line arguments
- pipes
- wildcards
- `cut`, `sort`, `uniq`
- `#!`

<!-- -------------------------------------------------------------------------------- -->

## Step 5: How are the concepts connected?

<em>

In this stage,
you put the formative assessments in a logical order,
then derive a point-form outline for the entire course from them.
This is also when you will consolidate the datasets your formative assessments have used.

Output: an instructional sequence and dataset summary.

Note:

- It is common to double back and change assessments in this stage
  so that they can share datasets,
  and/or to modify datasets to make them shareable.
- You are likely to discover things you forgot to list earlier during this stage,
  so don't be surprised if you have to double back a few times.
- The final outline should be at the chapter and lesson (video) level,
  i.e.,
  one major bullet point for each of the 4-5 chapters
  with 4-5 minor bullet points for the video lessons.

</em>

The chapter and lesson outline is:

1. Manipulating Files and Directories
   1. What a shell is; how it compares to a graphical interface.
   2. Basic commands (`whoami`; `pwd`; `ls`).
   3. Moving around (cd; the special paths `.` and `..`).
   4. Creating, deleting, and renaming (`cp`; `mv`; `rm`; `mkdir`; `rmdir`).
2. Manipulating Data
   1. Getting rows (`head`; `tail`).
   2. Getting columns (`cut`)
   3. Repeating steps (`history`; `!number` and `!command`)
   4. Selecting by value (`grep`; quoting arguments to protect special characters)
3. Combining Tools
   1. Redirection with `>`
   2. Piping with `|`
   4. Using the `*` and `?` wildcards
   3. Using `uniq` and `sort` (useful, and further examples of pipelines).
4. Batch Processing
   1. Storing commands in shell scripts.
   2. Permissions; using `!#`.
   3. Using arguments in shell scripts.
   4. Shell variables.
   5. Loops.

The datasets are:

- `./dental.csv`: two-column year and tooth data
- `./data/*.csv`: seasonal dental data ('autumn.csv', 'spring.csv', 'summer.csv', 'winter.csv')

<!-- -------------------------------------------------------------------------------- -->

## Step 6: Course outline

<em>

You are now ready to create a high-level course overview containing:

- a one-paragraph description (i.e., a sales pitch to students)
- learning objectives
- a summary of prerequisites

Doing this earlier often wastes effort,
since material is usually added, cut, or moved around in earlier steps.

Output: course description, learning objectives, and prerequisites.

Note: see the appendix for a discussion of how to write student-oriented learning objectives.

</em>

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

<!-- -------------------------------------------------------------------------------- -->

## Conclusion

As stated in the introduction,
this process is described as a one-way flow,
but in practice you will loop back repeatedly
as each stage informs you of something you overlooked.
Similarly,
you may add, move, or remove some specific items after you begin writing exercises
(though we must approve any significant structural changes to the course).
The end product,
though,
should have the flow described above,
since that is the order that will make it easiest for the next person who has to update your course
to understand what it is trying to achieve and why it is organized the way it is.

<!-- -------------------------------------------------------------------------------- -->

## Further Reading

- Huston: *[Teaching What You Don't Know][huston-teaching]*
- Lang: *[Small Teaching][lang-teaching]*
- Wilson: *[How to Teach Programming (and Other Things)][wilson-teaching]*

<!-- -------------------------------------------------------------------------------- -->

## Appendix: Writing Good Learning Objectives

A good learning objective is student-facing:
it explains what the student will do to demonstrate that they have learned
what you wanted them to learn.
The three elements of a good learning objective are:

1. The *main noun* (the thing you want students to master).
2. The *level of understanding* you want (discussed below).
3. An *observable verb*.
   "Student will understand X" isn't observable,
   but "student will summarize key steps in the creation of X" is.

The most widely used classification of levels of understanding is [Bloom's Taxonomy][bloom].
Its six levels and typical observable verbs are:

1. Knowledge: recalling learned information
   (name, define, recall).
2. Comprehension: explaining the meaning of information
   (restate, locate, explain, recognize).
3. Application: applying what one knows to novel, concrete situations
   (apply, demonstrate, use).
4. Analysis: breaking down a whole into its component parts
   and explaining how each part contributes to the whole
   (differentiate, criticize, compare).
5. Synthesis: assembling components to form a new and integrated whole
   (design, construct, organize).
6. Evaluation: using evidence to make judgments about the relative merits of ideas and materials
   (choose, rate, select).

[abela-chart]: http://extremepresentation.typepad.com/.shared/image.html?/photos/uncategorized/choosing_a_good_chart.jpg
[bloom]: https://en.wikipedia.org/wiki/Bloom's_taxonomy
[concept-map]: http://third-bit.com/teaching/memory.html#concept-maps
[datacamp-how]: https://www.datacamp.com/teach/documentation
[datacamp-teach]: https://www.datacamp.com/teach/documentation
[huston-teaching]: https://www.amazon.com/Teaching-What-You-Dont-Know/dp/0674035801/
[lang-teaching]: https://www.amazon.com/Small-Teaching-Everyday-Lessons-Learning/dp/1118944496/
[learner-profiles]: http://third-bit.com/teaching/lessons.html#learner-profiles
[profile-site]: https://github.com/datacamp/learner-profiles
[swc-teaching]: https://swcarpentry.github.io/instructor-training/
[teaching-statistics]: https://www.amazon.com/Teaching-Statistics-Tricks-Andrew-Gelman/dp/0198572247/
[tdd]: https://en.wikipedia.org/wiki/Test-driven_development
[uci-archive]: http://archive.ics.uci.edu/ml/index.php
[wilson-teaching]: http://third-bit.com/teaching/

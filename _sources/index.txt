.. Nova documentation master file, created by
   sphinx-quickstart on Wed Aug 31 17:54:08 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

CS323: Numerical Analysis and Computing
=======================================

Welcome to CS 323! This course is an introduction to the broad field of numerical
algorithms, optimization, and differential equations. Real-world examples from
different fields such as computer vision, machine learning, and data analysis will
be given alongside each topic to illustrate the wide applicability of the various
methods discussed in class. This course is heavy on programming, with the aim of
implementing most of the algorithms discussed in class. We will be using
`Python <https://www.python.org/>`_ along with its scientific computing packages
`NumPy <http://www.numpy.org/>`_ and `SciPy <https://www.scipy.org/>`_. While
there are many excellent resources available on the web, the following `lecture
notes <http://www.scipy-lectures.org/>`_ are particularly recommended. Of
course, we will be covering all the basics in class on an as needed basis. There is
**no required text** for this course, although some recommendations are given below.

| **Time:** 5PM - 8PM, Tuesdays, Fall 2017
| **Place:** Lucy Stone Hall Auditorium

| **Instructor:** `Mridul Aanjaneya <https://www.cs.rutgers.edu/~ma635/>`_
| **Office:** CBIM Room 18
| **Office hours:** Friday (4PM - 5PM)
| **Email:** mridul.aanjaneya@rutgers.edu

| **TA:** Carlos Muniz
| **Office:** Hill 270
| **Office hours:** Tuesday (3PM - 4PM) and also by appointment
| **Email:** cmm609@scarletmail.rutgers.edu

| **TA:** Mihee Lee
| **Office:** CBIM-cubic G
| **Office hours:** Monday (2PM - 3PM)  and also by appointment
| **Email:** ml1323@scarletmail.rutgers.edu

**Email Policy:** You are welcome to email the instructor about class-related
issues. Please start your subject line with \"**CS 323:**\". However, please do
not always count on an immediate reply. Although most questions will be answered
quickly, in the worst case you will receive a reply during (or shortly after)
the instructors' *next* scheduled office hours. It is also recommended to post
homework-related questions on `Piazza <https://piazza.com/class/j76v13g42b15y8>`_ instead of emailing the
instructor so that other fellow students can benefit from it.

**Grading Policy:** Grades will be awarded based on class participation, bi-weekly homeworks, two 75
minute in-class midterms and an **optional final**. The final grade will be computed as follows:

    55% x (homework grade) + 20% x (midterm1) + 20% x (midterm2) + 5% x (class participation)

**Final:** The final exam will have two parts, the first part corresponding to the
syllabus of midterm1, and the second part corresponding to the syllabus of
midterm2. When computing your
final grade, we will consider the **best** of the final and the corresponding
midterm score. This means that you can choose to *replace* either your score for midterm1,
or midterm2, or both by taking the final exam. However, if you do not perform
well in the final, your previous midterm scores will be used. The dates/times
for the midterm and final exams are listed below:

    * **Midterm 1:**
        * In-class Part (70%): 10/31 (5:15PM - 6:30PM)
        * Take-home Programming Part (30%): 11/03 (12PM) - 11/05 (11:55PM)
    * **Midterm 2:** 12/05 (5:15PM - 6:30PM)
    * **Final:** 12/20 (12PM - 3PM)

The in-class part of the midterm exams constitutes for 70% of
the midterm score, while the programming part constitutes for 30% of the midterm
score. Please note that the midterm and final exams are **open notes**, but all such
notes must be brought in **printed form**. The use of laptop computers, cell
phones, tablets, and other hand-held electronic devices is **strictly forbidden**.

**Class participation:** Participation in class will be
evaluated based on the number of classes attended, enthusiasm for answering the
instructor's questions, and willingness to help other students, both in person
and also online in the discussion forum. Extra credit points can also be earned
by helping the instructor improve his set of lecture notes. :-)

**Homework:** Students are encouraged to collaborate with each other on homework
problems in teams of size at most 3. However, they must individually turn in
their solutions and also mention the names of their collaborators on their
homework. All homework should be typed, and no two people should collaborate with each other on more than
two homeworks. We will not consider the lowest homework score when evaluating your
final grade. Homework problems will be posted every second week on this webpage,
and will be due at **midnight** on the Tuesday lecture two weeks later. Each
student is also granted **3 late days** total for submitting their homeworks.
After this grace period has expired (either for the current homework or from
previous homeworks) we will subtract 15% for each day that is delayed further.

**Typing resources:** All homework should be typed. Students can choose their favorite
platform for typing out their homework, some commonly used softwares are
`Microsoft Word <https://products.office.com/en-us/word>`_, `LaTeX <https://www.latex-project.org/get/>`_,
and `LyX <http://www.lyx.org/>`_. Thanks to a former student, Alex Ames, here is
a `LyX guide <https://www.cs.rutgers.edu/~ma635/courses/cs412-s15/lyx_guide/lyx_tips.pdf>`_
and associated `source files <https://www.cs.rutgers.edu/~ma635/courses/cs412-s15/lyx_guide/lyx_tips.zip>`_
used to generate it.

News and Announcements:
-----------------------

* (09/05) Discussion is now open on `Piazza <https://piazza.com/class/j76v13g42b15y8>`_.
* (09/05) There is no recitation on Thursday (09/07).
* (09/19) `Homework #1 <homeworks/homework1.html>`_ is out. Due on (10/03).
* (10/03) `Homework #2 <homeworks/homework2.html>`_ is out. Due on (10/17).
* (10/19) `Homework #1 Solutions <homeworks/hw1_solutions.pdf>`_ have been posted.
* (10/19) `Homework #3 <homeworks/homework3.html>`_ is out. Due on (11/01).
* (10/24) `Practice Midterm #1 <exams/practice_midterm1.pdf>`_ has been posted.
* (10/24) `Practice Midterm #1 Solutions <exams/practice_midterm1_solutions.pdf>`_ have been posted.
* (10/30) `Homework #2 Solutions <homeworks/hw2_solutions.pdf>`_ have been posted.
* (10/31) `Homework #4 <homeworks/homework4.html>`_ is out. Due on (11/14).
* (11/01) `Midterm #1 <exams/midterm1.pdf>`_ has been posted.
* (11/02) `Midterm #1 Solutions <exams/midterm1_solutions.pdf>`_ have been posted.
* (11/03) `Midterm #1 Programming <exams/midterm1_programming.html>`_ is out. Due on (11/05).
* (11/13) `Homework #3 Solutions <homeworks/hw3_solutions.pdf>`_ have been posted.
* (11/14) `Homework #5 <homeworks/homework5.html>`_ is out. Due on (11/28).
* (11/27) `Homework #4 Solutions <homeworks/hw4_solutions.pdf>`_ have been posted.
* (11/29) `Practice Midterm #2 <exams/practice_midterm2.pdf>`_ has been posted.
* (11/30) `Practice Midterm #2 Solutions <exams/practice_midterm2_solutions.pdf>`_ have been posted.
* (12/06) `Midterm #2 <exams/midterm2.pdf>`_ has been posted.
* (12/06) `Midterm #2 Solutions <exams/midterm2_solutions.pdf>`_ have been posted.
* (12/12) `Homework #5 Solutions <homeworks/hw5_solutions.pdf>`_ have been posted.

.. toctree::
    :numbered:
    :hidden:
    :maxdepth: 3

    Homework #1 <homeworks/homework1>
    Homework #2 <homeworks/homework2>
    Homework #3 <homeworks/homework3>
    Homework #4 <homeworks/homework4>
    Homework #5 <homeworks/homework5>
    Midterm #1 Programming <exams/midterm1_programming>

Contents:
---------

.. toctree::
    :numbered:
    :includehidden:
    :maxdepth: 3

    Introduction <intro>
    Vector and Matrix Algebra <algebra>
    Getting Started with Python <python>
    Linear Systems of Equations <linear>
    Non-linear Equations <nonlinear>
    Numerical Interpolation <interpolation>
    Accuracy of Interpolation and Splines <splines>

Coding Resources:
-----------------

1. `SciPy Lecture Notes <http://www.scipy-lectures.org/>`_

2. `Dive Into Python <http://www.diveintopython.net/>`_

Recommended Books:
------------------

1. J\. Solomon, `Numerical Algorithms <http://people.csail.mit.edu/jsolomon/share/book/numerical_book.pdf>`_, AK Peters/CRC Press, 2015\.
              
2. L\. N\. Trefethen and D\. Bau III, `Numerical Linear Algebra <http://bookstore.siam.org/ot50/>`_, SIAM, 1997\.

3. E\. Matthes, `Python Crash Course: A Hands-On, Project-Based Introduction to Programming <https://www.amazon.com/Python-Crash-Course-Hands-Project-Based/dp/1593276036>`_, No Starch Press, 2015\.


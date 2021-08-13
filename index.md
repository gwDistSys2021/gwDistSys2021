---
layout: home

---
<div class="wrapper" markdown="0"><div class="footer-col-wrapper">
<div class="footer-col two-col-1">
    <ul class="contact-list">
        <li><a href="https://faculty.cs.gwu.edu/timwood"><b>Prof. Tim Wood</b></a></li>
        <li><a href="mailto:timwood@gwu.edu">timwood@gwu.edu</a></li>
        <li>Office Hours: Tuesdays 1pm, check #office-hours</li>
        <li>Section 10</li>
        <li><i>Graders</i>: Huadong Hu and Guodong Xie</li>

    </ul>
</div>
<div class="footer-col two-col-2">
    <ul class="contact-list">
        <li><b>Prof. Roozbeh Haghnazar</b></li>
        <li><a href="mailto:roozbeh@gwu.edu">roozbeh@gwu.edu</a></li>
        <li>Office Hours: Fridays 2pm, check #office-hours</li>
        <li>Section 11</li>
        <li>Grader Office hours: Mondays 7pm</li>
    </ul>
    </div>
</div></div>

> This course will be an in-depth study of the algorithmic and implementation challenges in building large scale distributed applications. Topics include distributed coordination, scheduling, consistency issues, and fault tolerance algorithms. The course will cover how fundamental distributed systems concepts are applied to cloud computing environments. The course will mix algorithmic concepts and practical implementations; substantial programming experience is required.




## Announcements ##
- The exam will be online during class Thursday November 12
- The [Final Project](/project/) Milestone 0-1 details have been announced.
- If you have feedback for us, please [fill out this anonymous form!](https://forms.gle/veNaFvyrwggT2HZbA)
- Check the [Syllabus](syllabus/) for more info.
- Both sections 10 and 11 of CSCI 6421 will meet together *as one class*. You can register for either section with no difference. 
- *We will meet online using Blackboard Collaborate Ultra*. If we have problems with Blackboard, check here or on [Slack](https://join.slack.com/t/gwdistsys20/signup) for a backup plan!
- The course will use the Go programming language. Get ready to code!


<hr>

## Schedule  ##

All deadlines are 11:59PM Eastern Time

<div style="font-size:90%">

<table>
    <thead>
    <tr><th style="text-align:center" colspan="2">Part 1: Building Blocks</th></tr>
    </thead>
    <tr><td style="width:20%"><b>Overview</b>
    <br>9/3/2020
    </td><td>
    <a href="/slides/1-introduction.pdf">Lecture Slides</a> and <a href="https://blackboard.gwu.edu/webapps/collab-ultra/tool/collabultra?course_id=_342915_1&amp;mode=cpview">Video</a> (on BlackBoard Collaborate click the Menu icon and go to Recordings)<br>
    </td>
    </tr>
    <tr><td style="text-align:right"><i>Tasks:</i></td>
    <td>
    <a href="https://join.slack.com/t/gwdistsys20/signup">Join Slack</a> today! -- <a href="https://forms.gle/yd45FuMR7HSBJvMs9">Student Survey</a> due Monday 9/7 
    </td>
    </tr>
    <tr><td><b>Scalable Execution</b>
    <br>9/10/2020
    </td><td><a href="/slides/2-execution.pdf">Lecture Slides</a> and <a href="https://blackboard.gwu.edu/webapps/collab-ultra/tool/collabultra?course_id=_342915_1&amp;mode=cpview">Video</a>  </td>
    </tr>
    <tr><td style="text-align:right"><i>Tasks:</i></td> 
    <td><a href="/readings.html">Readings in Chapters 1, 3</a> -- Watch <a href="https://gwu.box.com/s/uykp9ouz6fqc8d3psmehq46swmn7i4gm">Azure HWaaS Video</a> -- <a href="hw1/">HW1: Parallel Sum</a> due Tuesday 9/15</td>
    </tr>
    <tr><td><b>Communication</b>
    <br>9/17/2020
    </td><td><a href="/slides/3-communication.pdf">Lecture Slides</a> and <a href="https://blackboard.gwu.edu/webapps/collab-ultra/tool/collabultra?course_id=_342915_1&amp;mode=cpview">Video</a> </td>
    </tr>
    <tr><td style="text-align:right"><i>Tasks:</i></td> 
    <td><a href="/readings.pdf">Readings in Chapters 3, 4</a> -- Read <a href="http://research.google.com/archive/mapreduce-osdi04.pdf">MapReduce paper</a></td>
    </tr>
    <tr><td><b>Architectures</b>
    <br>9/24/2020
    </td><td><a href="/slides/4-architecture.pdf">Lecture Slides</a> and <a href="https://blackboard.gwu.edu/webapps/collab-ultra/tool/collabultra?course_id=_342915_1&amp;mode=cpview">Video</a>  </td>
    </tr>
    <tr><td style="text-align:right"><i>Tasks:</i></td> 
    <td> <a href="/readings.pdf">Readings in Chapter 2</a>  </td>
    </tr>
    <tr><td><b>Resource Management</b>
    <br>10/1/2020
    </td><td><a href="/slides/5-resources.pdf">Lecture Slides</a> and <a href="https://blackboard.gwu.edu/webapps/collab-ultra/tool/collabultra?course_id=_342915_1&amp;mode=cpview">Video</a>  </td>
    </tr>
    <tr><td style="text-align:right"><i>Tasks:</i></td> 
    <td> <a href="hw2/">HW2: Map Reduce</a> due 10/1, -10 points by 10/8 -- <a href="https://youtu.be/ZcaQ7yLAYwM">MapReduce Help Video</a> </td>
    </tr>
    <tr><td><b>Resource Management 2</b>
    <br>10/8/2020
    </td><td><a href="/slides/6-migration.pdf">Lecture Slides</a> and <a href="https://blackboard.gwu.edu/webapps/collab-ultra/tool/collabultra?course_id=_342915_1&amp;mode=cpview">Video</a>  </td>
    </tr>
    <tr><td style="text-align:right"><i>Tasks:</i></td> 
    <td> <a href="hw2/">HW2: Map Reduce</a> -10 points by 10/8 -- <a href="https://forms.gle/bCMJnDwNzhDudEGo6">Partner Feedback Form</a> </td>
    </tr>
</table>

<table>
    <thead>
    <tr><th style="text-align:center" colspan="2">Part 2: Principles of Distributed Systems</th></tr>
    </thead>
    <tr><td style="width:20%"><b>Clocks and Timing</b>
    <br>10/15/2020
    </td><td>
    <a href="/slides/7-coordination-notes.pdf">Lecture Slides</a> and <a href="https://blackboard.gwu.edu/webapps/collab-ultra/tool/collabultra?course_id=_342915_1&amp;mode=cpview">Video</a> -- <a href="/clock-worksheet.pdf">Clock Worksheet</a> and <a href="https://youtu.be/IAI712Kk-O8">Solution Video</a>
    </td>
    </tr>
    <tr><td style="text-align:right"><i>Tasks:</i></td>
    <td><a href="/readings.pdf">Readings in Chapter 6</a> -- <a href="/project/#milestone-1-select-a-topic">Milestone 1: Select a Topic</a> - 10/19</td>
    </tr>
    <tr><td><b>Distributed Coordination</b>
    <br>10/22/2020
    </td><td><a href="/slides/8-consensus.pdf">Lecture Slides</a> and <a href="https://blackboard.gwu.edu/webapps/collab-ultra/tool/collabultra?course_id=_342915_1&amp;mode=cpview">Video</a></td>
    </tr>
    <tr><td style="text-align:right"><i>Tasks:</i></td>
    <td><a href="/readings.pdf">Readings in Chapter 6</a> </td>
    </tr>
    <tr><td><b>Fault Tolerance</b><br>10/29/2020</td>
    <td><a href="/slides/9-ft-notes.pdf">Lecture Slides</a> and <a href="https://blackboard.gwu.edu/webapps/collab-ultra/tool/collabultra?course_id=_342915_1&amp;mode=cpview">Video</a> </td>
    </tr>
    <tr><td style="text-align:right"><i>Tasks:</i></td>
    <td><a href="/readings.pdf">Readings in Chapter 8</a> -- <a href="/project/#milestone-2-literature-review">Milestone 2: Literature Review</a> - 10/29</td>
    </tr>
    <tr><td><b>Replication</b><br>11/5/2020</td>
    <td><a href="/slides/10-consistency-notes.pdf">Lecture Slides</a> and <a href="https://blackboard.gwu.edu/webapps/collab-ultra/tool/collabultra?course_id=_342915_1&amp;mode=cpview">Video</a> -- <a href="slides/10-consistency-problems.pdf">Consistency Problems Worksheet</a> </td>
    </tr>
    <tr><td style="text-align:right"><i>Tasks:</i></td>
    <td><a href="/readings.pdf">Readings in Chapter 7</a> -- <a href="/project/#milestone-3-design-document">Milestone 3: Design Document</a> - 11/8 (extended)</td>
    </tr>
    <tr><td><b>Midterm Exam</b><br>11/12/2020</td>
    <td><a href="exam/sample-exam.pdf">Practice problems</a></td>
    </tr>
    <tr><td style="text-align:right"><i>Tasks:</i></td><td>Study!</td></tr>
</table>

<table>
    <thead>
    <tr><th style="text-align:center" colspan="2">Part 3: Distributed Systems in Practice</th></tr>
    </thead>
    <tr><td style="width:20%"><b>Performance Modeling</b><br>11/19/2020</td>
    <td><a href="/slides/11-performance.pdf">Lecture Slides</a> and <a href="https://blackboard.gwu.edu/webapps/collab-ultra/tool/collabultra?course_id=_342915_1&amp;mode=cpview">Video</a></td>
    </tr>
    <tr><td style="text-align:right"><i>Tasks:</i></td><td>Work on your project! </td></tr>
    <tr><td><b>Cloud Computing</b><br>12/3/2020</td>
    <td><a href="/slides/12-cloudapps.pdf">Lecture Slides</a> and <a href="https://blackboard.gwu.edu/webapps/collab-ultra/tool/collabultra?course_id=_342915_1&amp;mode=cpview">Video</a></td>
    </tr>
    <tr><td style="text-align:right"><i>Tasks:</i></td><td>Work on your project! </td></tr>
    <tr><td><b>Internet of Things and Big Data</b><br>12/10/2020</td>
            <td><a href="/slides/13-big-data-iot-ml.pdf">Lecture Slides</a> and <a href="https://blackboard.gwu.edu/webapps/collab-ultra/tool/collabultra?course_id=_342915_1&amp;mode=cpview">Video</a></td>
    </tr>
    <tr><td style="text-align:right"><i>Tasks:</i></td><td>
    <a href="/project/#milestone-4-final-report">Milestone 4: Final Report</a> - 12/14 -- <a href="/hw3/">Bonus HW3: Leader Election</a> - 12/10
    </td></tr>
</table>

</div>

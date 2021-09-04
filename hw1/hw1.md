---
layout: page
title: "HW1: Parallel Sum"
permalink: /hw1/
---

> Deadline: Tuesday 9/17/2020
> GitHub Repo Setup: [https://classroom.github.com/a/4Mb4nNod](https://classroom.github.com/a/4Mb4nNod)
> 
> This assignment must be completed **individually**. You **MAY NOT** share your code for this assignment with any other student. It is acceptable to provide high level advice about relevant go libraries and tools, but you should not be explaining to other students how to solve the problem, nor should you be searching the internet for solutions.

## Overview 
In this assignment you will solve a simple problem to familiarize you with golang, especially with Goroutine, http, and RPC. The Go web site contains lots of tutorial information and this might be helpful to you if you are new with Golang. https://tour.golang.org/

### Go Setup and Dev Environment

We recommend that you work on the assignment on your own machine so that you can use the tools, text editors, etc. that you are already familiar with. 
If you haven’t installed Golang on your own machine, visit here to install it https://golang.org/doc/install. 

If you haven't used Go, you can take the [Go Tour](https://tour.golang.org/list) or find many other tutorials and documents online.

We will grade your labs using Go version 1.14; you should use 1.14 too. You can check your Go version by running `go version` -- if you have a more recent version that is OK too.

We recommend writing your code in [Visual Studio Code](https://code.visualstudio.com/). In order to get help from the course instructors, you must be using Visual Studio Code and have the [Live Share](https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare) plugin installed which will allow you to share your environment. A very incomplete setup document is [provided here](/hw1/setup/) (improve it for extra credit!).

### GitHub

We will use GitHub Classrooms to manage your repositories and submit code. You must create a (free) GitHub account if you do not already have one. Use the link at the top of this page to create your repository.

You should also use this assignment to practice using git and GitHub. *You must create at least one commit and push your code to GitHub for each of the phases listed below to receive full credit.*

---

## Parallel Sum
You will write code to parallelize the task of summing up a list of numbers stored in a large file. Summation is not very computationally intensive, but you can imagine replacing this with a more complicated task such as performing image recognition on a large set of files, or performing sentiment analysis on a large number of tweets. We will solve this problem in three phases of increasing complexity. You must solve all of them for full credit.

> **Output:** Your programs can display any debugging output you need when you are developing, but the version you submit for grading should not contain any debugging info. For each phases, the output function code has been implemeted for you, and you should not make any changes to it. You can assume that the input file is formatted correctly.

## Phase 1: Sequential Sum
To start with, you must complete our starter code to correctly sum a list of numbers from a file without using any parallelism.

You are provided three files in the  `sequential_sum/` starter code:
  - `main.go` - contains the main entrance to your program. It should determine the file to be processed as a command line argument such as `-f test1.txt`. It then should invoke a function in the `sum.go` file to perform the sum.
  - `sum.go` - implements the core `Sum(fileName string)` function which must return . You should fill in your code here, but should not change the signature of this function. The file also contains a `readInts` function which you should use to turn a file into an array of integers for processing by your Sum function.
  - `sum_test.go` - includes several test cases to validate that your program works correctly. You can extend this file if you would like to add more test cases. 

You can build, run, and test your program with:
```
go build -o seq

./seq -f test1.txt
-83

go test
```

Hints:
  - This should be pretty easy. Just learn how to use for loops and addition
  - Lookup how to have go process command line arguments

> **IMPORTANT:** At this point you should be sure to commit your code and push it to github. As you make progress on the following phases you should commit and push your code regularly. Failure to do so may cause you to lose points.

## Phase 2: Goroutines
Summing numbers is fairly trivial to implement in a sequential way, so next you must make it parallel. This will help you understand concurrency and communication mechanisms in Golang which are fundamental in future more complicated assignments.

Next work on the files in `parallel/`. Your new program should extend the files in the following ways:
  - `main.go` - should now accept a second argument `-g` which specifies how many goroutines should be started to execute the summation in parallel.
  - `sum.go` - modifies the `Sum()` function to accept the number of goroutines to use. You should still use the `readInts` function to sequentially read the file, but then you must split up the sum across the specified number of threads.
  - `sum_test.go` - similar to above

You can build, run, and test your program with:
```
go build -o parallel

./parallel -f test1.txt -g 4
-83

go test
```

Hints:
  - Learn about goroutines
  - Learn about go channels for communication

## Phase 3: HTTP/RPC + Goroutines
Finally, we will make our summation program accessible over a remote interface. HTTP is the standard interface used in the web to allow external clients to communicate with a service. Remote Procedure Calls (RPC) are another form of communication which offers more flexibility to the programmer. In this phase you will extend your program to run an HTTP Server which accepts client requests from a web browser; the server then uses RPC to pass the request to the go program which will compute the sum. This is a common 2-tier web application architecture with a web frontend and an application server backend.

In a real implementation, the HTTP frontend would allow users to upload files to be processed. For simplicity, we will just have the user access a URL that specifies the file name to be processed, e.g., `http://localhost:8080/?f=test1.txt&g=10`. We will assume the RPC backend has access to this file.

You will work on the files in `http_parallel/` for this phase. You are provided starter code for the two servers:
  - `http_front/` - contains the files for running an HTTP server that listens on port 8080. The sample code starts a simple HTTP server and displays the requested URL. You must extend this to make an RPC to the backend specifying the file to be analyzed. After the sum is complete it should output the result such as `test1.txt-1--83`
  - `rpc_back/` - contains the files for the RPC server backend that listens on port 8083. It should receive RPC requests indicating the file to be processed and and the number of goroutines to perform the sum. It should then return the summation result to the frontend.

You can build and start your program using *two* terminals:
```
## RPC Server -- Terminal 1
cd rpc_back/
go build  -o rpc
./rpc
RPC Listening on port 8083
...
## HTTP Server -- Terminal 2
cd http_front/
go build -o http
./http
HTTP Listening on port 8080

```

You can then test your servers by accessing them with a web browser: [http://localhost:8080/?f=test1.txt&g=1](http://localhost:8080/?f=test1.txt&g=1)

Or you can test using the curl command line utility:
```
curl --request GET -sL  --url 'http://localhost:8080/?f=test1.txt&g=1'
{"file_name":"test1.txt","go_routine_nums":1,"sum":-83}
```
Hints:
  - Make sure you run both the front and back programs!
  - The starter code provides a basic RPC example and starts the HTTP server for you
  - Learn how to process an HTTP request to extract fields in the URL
  - You can test your program either with Curl or a real web browser
  - Always verify that your code has been pushed to github by checking your commits on the web interface!

## Submission and Grading
When you are finished with your assignment follow these steps:

  1. Make sure your code doesn't have any extraneous outputs and matches the requirements above
  2. Commit and Push your code, check the github interface to be sure it is there
  3. (Optional) You can check whether your code passes our test cases on the GitHub website by going to Actions -> Autograding and then checking the `Run education/autograding@v1` test. If any part of the test fails, then the whole test will be marked as failed. However, when grading we will check each test individually.
  4. (**IMPORTANT**) Go to the Issues page of your repository and create a new Issue. The title of the issue should be your full name. Add a comment that says `@HuadongHu code is ready to review`.  If any aspects of your code are incomplete or not working, you should explain which parts have a problem in your comment.

Failure to follow the above steps will cause you to lose points.

**Rubric:** Your assignment will be graded as follows
```
X / 4:  Sequential sum basic requirements (command line arguments, output format, code quality, etc) 
X / 6:  Sequential sum works correctly
X / 4:  Parallel sum basic requirements (command line arguments, output format, code quality, etc)
X / 12: Parallel sum works correctly
X / 4:  HTTP/RPC basic requirements (http/grpc status, code quality, etc)
X / 15: HTTP/RPC sum works correctly
X / 5:  GitHub used correctly
=======
XX / 50 total points
```

**Late Policy:** Late submissions will lose 5 points (out of 50) per 24 hour period after the deadline (i.e., submitting one hour late is -5, submitting 25 hours late is -10, etc). If you make any commits to your repository after the deadline, the submission will be considered late unless you have already coordinated this with the instructors.
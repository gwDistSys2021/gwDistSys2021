---
layout: page
title: "HW 3: Leader Election"
permalink: /hw3/
---

> Deadline: Thursday 12/10/2020 
>
> GitHub Repo Setup: [https://classroom.github.com/g/iWrPYTjH](https://classroom.github.com/g/iWrPYTjH)
>
> This assignment must be completed **individually**. You may discuss the concepts of the project with other students *but you may **not** share any code!*.
>
> This assignment is a **bonus** assignment. You will get a grade out of 20 points which will then be added as a bonus to your grade from HW2.

In this project you will implement a Leader Election algorithm in Go. Your algorithm must be based on the protocol defined in the Raft Consensus system, which is able to handle crash failures of leaders and other nodes in the system.  Raft's leader election is based on the Bully Algorithm covered in class, and uses the idea of terms and randomized timers to trigger elections. The [Raft paper](raft-extended.pdf) gives a detailed explanation of its algorithms, although you only really need to understand the Election portion. Hint: Figure 2 is very helpful, but you will need to separate out the parts about creating log entries (which we don't care about) vs heartbeats and elections (which you must implement).

The project is adapted from MIT's 6.824 Distributed Systems course. Their assignment includes the full Raft Consensus protocol, but we will only do the first stage which focuses on leader election. You must implement the functions necessary to allow a candidate node to start an election and receive votes from other nodes. An elected leader should send heartbeat messages to remain leader, and if it fails, then a new election should begin.

We supply you with skeleton code `src/raft/raft.go`. We also supply a set of tests, which you should use to drive your implementation efforts, and which we'll use to grade your submitted lab. The tests are in `src/raft/test_test.go`. The starter code also includes a special RPC library which gives us support to cause arbitrary failures of nodes during a test. You must use this library (it has the same basic interface to what we've used before).

To get up and running, execute the following commands. 

```bash
$ cd src/raft
$ go test
TestInitialElection: ...
--- FAIL: TestInitialElection (4.96s)
    config.go:334: expected one leader, got none
TestPreviousLeaderRejoin: ...
--- FAIL: TestPreviousLeaderRejoin (4.95s)
    config.go:334: expected one leader, got none
TestReElectionFail: ...
--- FAIL: TestReElectionFail (4.97s)
    config.go:334: expected one leader, got none
TestReElectionSuccess: ...
--- FAIL: TestReElectionSuccess (5.14s)
    config.go:334: expected one leader, got none
...
$
```
This output shows that the starter code is working, but that it can't yet elect any leaders.

## The code
You must implement Raft's Leader Election by adding code to `raft/raft.go`. In that file you'll find skeleton code, plus examples of how to send and receive RPCs.

Your implementation must support the following interface, although some of these functions will not be used for the Election phase. You'll find more details in comments in `raft.go`. 

```go
// create a new Raft server instance:
rf := Make(peers, me, persister, applyCh)

// ask a Raft for its current term, and whether it thinks it is leader
rf.GetState() (term, isLeader)

```

A service calls `Make(peers,me,...)` to create a Raft peer. The peers argument is an array of network identifiers of the Raft peers (including this one), for use with RPC. The `me` argument is the index of this peer in the peers array. In practice you will never call this yourself - the test cases will call this to setup several nodes and automatically configure the network connections between them.

`raft.go` contains example code that sends an RPC (`sendRequestVote()`) and that handles an incoming RPC (`RequestVote()`). Your Raft peers should exchange RPCs using the `labrpc` Go package (source in `src/labrpc`). The tester can tell `labrpc` to delay RPCs, re-order them, and discard them to simulate various network failures. While you can temporarily modify `labrpc`, make sure your Raft works with the original `labrpc`, since that's what we'll use to test and grade your lab. Your Raft instances must interact only with RPC; for example, they are not allowed to communicate using shared Go variables or files. 

## Your Task: Leader Election
Implement Raft leader election and heartbeats (`AppendEntries` RPCs with no log entries). The goal is for a single leader to be elected, for the leader to remain the leader if there are no failures, and for a new leader to take over if the old leader fails or if packets to/from the old leader are lost. 

> The source code you've been provided is for an assignment that implements the full Raft protocol. We've removed many of the methods we won't use, but some are still there. You should focus on the sections of code referred to as `2A` (since this was the election phase of the original assignment).  You won't need to implement pieces referred to as `2B` or `2C`.

### Hints:
  - You can't easily run your Raft implementation directly; instead you should run it by way of the tester, i.e. `go test -run ${test_name}`(could be `TestInitialElection`, `TestPreviousLeaderRejoin`, `TestReElectionFail`, `TestReElectionSuccess`, `TestReElectionSuccess2`).
  - Follow the paper's Figure 2. At this point you care about sending and receiving RequestVote RPCs, the Rules for Servers that relate to elections, and the State related to leader election,
  - Add the Figure 2 state for leader election to the`Raft` struct in `raft.go`. 
  - Fill in the `RequestVoteArgs` and `RequestVoteReply` structs. Modify `Make()` to create a background goroutine that will kick off leader election periodically by sending out `RequestVote` RPCs when it hasn't heard from another peer for a while. This way a peer will learn who is the leader, if there is already a leader, or become the leader itself. Implement the `RequestVote()` RPC handler so that servers will vote for one another.
  - To implement heartbeats, define an `AppendEntries` RPC struct (though you may not need all the arguments defined in the paper), and have the leader send them out periodically. Write an `AppendEntries` RPC handler method that resets the election timeout so that other servers don't step forward as leaders when one has already been elected.
  - Make sure the election timeouts in different peers don't always fire at the same time, or else all peers will vote only for themselves and no one will become the leader.
  - The tester requires that the leader send heartbeat RPCs no more than ten times per second.
  - The tester requires your Raft to elect a new leader within five seconds of the failure of the old leader (if a majority of peers can still communicate). Remember, however, that leader election may require multiple rounds in case of a split vote (which can happen if packets are lost or if candidates unluckily choose the same random backoff times). You must pick election timeouts (and thus heartbeat intervals) that are short enough that it's very likely that an election will complete in less than five seconds even if it requires multiple rounds.
  - The paper's Section 5.2 mentions election timeouts in the range of 150 to 300 milliseconds. Such a range only makes sense if the leader sends heartbeats considerably more often than once per 150 milliseconds. Because the tester limits you to 10 heartbeats per second, you will have to use an election timeout larger than the paper's 150 to 300 milliseconds, but not too large, because then you may fail to elect a leader within five seconds.
  - You may find Go's [rand](https://golang.org/pkg/math/rand/) useful.
  - You'll need to write code that takes actions periodically or after delays in time. The easiest way to do this is to create a goroutine with a loop that calls [time.Sleep()](https://golang.org/pkg/time/#Sleep). Don't use Go's `time.Timer` or `time.Ticker`, which are difficult to use correctly.
  - Read this advice (from MIT) about [locking](raft-locking.txt) and [structure](raft-structure.txt).
  - If your code has trouble passing the tests, read the paper's Figure 2 again; the full logic for leader election is spread over multiple parts of the figure.
  - Don't forget to implement `GetState()`.
  - The tester calls your Raft's `rf.Kill()` when it is permanently shutting down an instance. You can check whether `Kill()` has been called using `rf.killed()`. You may want to do this in all loops, to avoid having dead Raft instances print confusing messages.
  - A good way to debug your code is to insert print statements when a peer sends or receives a message, and collect the output in a file with `go test -run ${test_name} > out`. Then, by studying the trace of messages in the `out` file, you can identify where your implementation deviates from the desired protocol. You might find `DPrintf` in `util.go` useful to turn printing on and off as you debug different problems.
  - Go RPC sends only struct fields whose names start with capital letters. Sub-structures must also have capitalized field names (e.g. fields of log records in an array). The `labgob` package will warn you about this; don't ignore the warnings.
  - Check your code with `go test -race`, and fix any races it reports.

Be sure you pass the all tests before submitting, so that you see something like this:

```
$ go test
TestInitialElection: ...
  ... Passed --   3.1  3   88   14814    0
TestPreviousLeaderRejoin: ...
  ... Passed --   3.6  3   27    3912    0
TestReElectionFail: ...
  ... Passed --   4.5  3   35    3714    0
TestReElectionSuccess: ...
  ... Passed --   5.5  3   51    6510    0
TestReElectionSuccess2: ...
  ... Passed --   7.7  5  179   22214    0
PASS
ok      raft    10.187s
$
```

Each "Passed" line contains five numbers; these are the time that the test took in seconds, the number of Raft peers (usually 3 or 5), the number of RPCs sent during the test, the total number of bytes in the RPC messages, and the number of log entries that Raft reports were committed. Your numbers will differ from those shown here. You can ignore the numbers if you like, but they may help you sanity-check the number of RPCs that your implementation sends. The grading script will fail your solution if it takes more than 600 seconds for all of the tests (`go test`), or if any individual test takes more than 120 seconds. 

## Submission

Push your finalized code to github when you finish and: 

  1. Make sure your code doesn't have any extraneous outputs and matches the requirements above. Remember to remove any intermediate files and the compiled binary file. You can modify [.gitignore](https://git-scm.com/docs/gitignore) file to intentionally ignore these files. Your repository will be graded in part on its cleanliness. 
  2. Commit and Push your code, check the github interface to be sure it is there
  3. (**IMPORTANT**) Go to the Issues page of your repository and create a new issue titled `Raft Submission` with the following information:
  * Your name
  * If any aspects of your code are incomplete or not working, you should explain which parts have a problem.
  * Then tag the graders in the issue using their github usernames (`@HuadongHu and @freebyron`).

**Important:** As with all assignments, it is an academic integrity violation to share your code with other students or to get a solution (full or partial) from another source. Since students may be submitting their code at different times, it is extra important to keep your code to yourself!


**Late Policy:** This assignment cannot be submitted late.

> **Acknowledgments:** This assignment is adapted from the MIT 6.824 Distributed Systems course, which was developed by Robert Morris, Frans Kaashoek, and Nickolai Zeldovich.
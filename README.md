# Implementing Raft Logic in Go

This project involves implementing a simplified version of the Raft consensus algorithm in Go. The primary goal is to demonstrate leader election and log replication using the Raft protocol in a simulated environment.

## Table of Contents

   1. [Introduction](#introduction)
   2. [Prerequisites](#prerequisites)
   3. [Project Structure](#project-structure)
   4. [Getting Started](#getting-started)
   5. [Implementation Details](#implementation-details)
   6. [Running the Tests](#running-the-tests)
   7. [Expected Behavior and Logs](#expected-behavior-and-logs)
   8. [Contact](#For-queries,-contact:)

## Introduction

Raft is a consensus algorithm designed to be easy to understand. This project implements key functionalities of Raft, including leader election and log replication, to provide fault tolerance in a distributed system. The implementation includes handling scenarios like network partitioning and node recovery.
Prerequisites

   * Go (Golang) 1.16 or later installed on your system. Install Go.
   * Familiarity with Go programming language and basic understanding of distributed consensus algorithms.
   * Understanding of the Raft consensus algorithm. You can refer to the Raft paper and the interactive visualization.

## Project Structure

The project directory is organized as follows:

```
.
├── go.mod
├── NodeLogs
│   ├── 0
│   ├── 1
│   ├── 2
│   ├── 3
│   └── 4
├── raft_cluster.go
├── raft_election_logic.go
├── raft_leader_logic.go
├── raft_node.go
├── raft_rpc_handlers.go
├── raft_test.go
├── README.md
├── server_setup.go
└── verbose
    ├── 1.log
    └── 2.log

```

   * raft_cluster.go: Handles cluster management and node interactions.
   * raft_election_logic.go: Contains the logic for leader election.
   * raft_leader_logic.go: Manages the leader's responsibilities, including log replication.
   * raft_node.go: Defines the state and behavior of a Raft node.
   * raft_rpc_handlers.go: Handles Remote Procedure Calls (RPC) for node communication.
   * server_setup.go: Sets up the server environment for the cluster.
   * NodeLogs/: Contains log files for each node.
   * verbose/: Directory for detailed test logs.

## Getting Started

1. Install Go: Follow the official [Go installation guide](https://go.dev/doc/install) to set up Go on your system.
2. Clone the Repository:
```
git clone https://github.com/harshapatil7/Implementing-Raft-Logic-in-Go.git
cd raft-implementation
```
3. Build the Project:
```
go build
```

Run the Tests: You can run specific tests using:
```
    go test -v -run Test1 > verbose/1.log
    go test -v -run Test2 > verbose/2.log
```

## Implementation Details

### The following key functionalities are implemented:

   1. becomeFollower Function: Handles the transition of a node to the follower state.
   2. RequestVote Handler: Manages the logic for a follower node to handle incoming RequestVote RPCs from candidates.
   3. Candidate Vote Handling: Handles replies to RequestVote RPCs, managing election results for candidates.
   4. Leader Commit Logic: Manages the leader's log commitment process upon receiving majority confirmations.

## Running the Tests

### Tests are provided to simulate different scenarios:

   * Test1: Simple leader election scenario. Tests if a leader is correctly elected and handles network partitions.
   * Test2: Replication failure scenario where a leader is disconnected after committing some commands.
   * Test3: More complicated leader election scenario with intentional failure to observe Raft's behavior.
   * Test4: Log replication failure scenario where the leader drops without committing and rejoins later.

Run tests using the go test command as mentioned in the Getting Started section.

## Expected Behavior and Logs

### Each test generates logs that provide insights into the Raft cluster's state changes. Logs are stored in the verbose/ directory and the NodeLogs/ directory.

   Verbose Logs: Contain detailed outputs for each test run.
   Node Logs: Show individual node behavior and state transitions, useful for understanding leader elections, log replications, and network partition handling.

**Known Issues**

   Test3 Failure: Test3 is designed to fail by default. This is an intentional behavior to demonstrate a situation where no leader can be elected due to insufficient nodes. Uncomment the sleep line in Test3 to allow it to pass by giving enough time for a leader to be elected.



## **In this project, you will:**

1. Learn the basics of GoLang.
2. Understand the basic logic behind Raft
3. Implement part of the logic behind raft, in GoLang, for leader election and log replication.

## **What you're given:**

You are provided with a GoLang project structure, which, when complete, will allow you to successfully demonstrate leader election and log replication via Raft. However, parts of the code are deliberately missing; Your job is to fill it in, and make sure that expected behaviour is observed in scenarios such as network partitioning.
```
.
├── go.mod
├── NodeLogs
│   ├── 0
│   ├── 1
│   ├── 2
│   ├── 3
│   └── 4
├── raft_cluster.go
├── raft_election_logic.go
├── raft_leader_logic.go
├── raft_node.go
├── raft_rpc_handlers.go
├── raft_test.go
├── README.md
├── server_setup.go
└── verbose
    ├── 1.log
    └── 2.log
```

The files server\_setup.go, raft\_node.go and raft\_cluster.go require no modification. raft\_node.go, however, contains vital information about the persistent state of a raft node itself, and is worth going through to better understand the flow of the code.

## ** Things you go through before starting **

Once you've installed Go, it's a good idea to familiarise yourself with Raft. [The Raft Paper](http://raft.github.io/raft.pdf) itself, in conjunction with the interactive visualisation at [https://raft.github.io/](https://raft.github.io/), is a major help there.

Familiarise yourself with Raft Leader Election and Log Replication, i.e up until but not including Section 7 of the paper; you **do not** need to familiarise yourself with Log Compaction.

The scenarios we deal with here do not include complete node failure, although it is trivial to account for such a case by asking recovered nodes to replay their logs. Instead, we deal with **partitioned** nodes; i.e, a 'disconnected node' is a node that is still functioning, but is cut off from the rest of the cluster. Think along the lines of 'its internet failed.' **KNOWING THIS IS IMPORTANT FOR YOUR EVALUATION.**

If you don't understand why the test case are failing please go through the test case file and read comments

## **For queries, contact:**

**Harsha Patil:** [**harshapatil.hp01@gmail.com**](mailto:harshapatil.hp01@gmail.com)

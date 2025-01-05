# Go Race Condition in Concurrent Counter

This repository demonstrates a race condition in a Go program that uses goroutines and a mutex to increment a shared counter.  The program aims to sum the numbers from 0 to 999, but due to a subtle error in the goroutine handling, it might produce an incorrect result.  The solution demonstrates how to fix this race condition.

## Bug

The `bug.go` file contains the buggy code. The main issue is that while a mutex is used to protect access to the `count` variable, the loop creating the goroutines captures `i` by reference, meaning all the goroutines operate on the final value of `i` (999) rather than their own copy.

## Solution

The `bugSolution.go` file presents a corrected version.  The key change is that we explicitly pass a copy of `i` into the goroutine, thereby resolving the race condition and ensuring each goroutine works with its own unique value of `i`.
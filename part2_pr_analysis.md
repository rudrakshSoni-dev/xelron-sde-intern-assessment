# Part 2: Pull Request Analysis

**Repository Selected:** `/aio-libs/aiokafka`

## Task 2.1: PR Selection and Comprehension

### PR Selection
I chose AIOkafka because the PRs looked familiar where there are typing changes, and also involved refactoring of existing codebase, something I am more confident about.

### 1. Analysis of PR #1006
**PR Summary:** The repo has already well-written code and all the unit tests were also written properly. This PR only added type safety ,and improves readablity of the code.

The codebase as appears to be is written using traditional / outdated coding syntaxes and appreoaches.This PR fixes all the errors and type errors in their `/records` and `/coordinator` sub-repos.

The syntaxes in many files don't match that of modern dependencies, thus this PR resolves all the type errors due to redundant techniques used previously by maintainers.

Some minor feature additions were also there like using of TypeIS middleware.


**Technical Changes:**
* `aiokafka/record/` 

-> 094cb23 & 85a0415 : Added typing in the existing codebase, implemented cython functions for structured more modular code.

-> b1efa77 : fixed various type errors accross various files over the repo.

-> 7fa1efa & 58bc26c : implemented w/o protocol feature and in the next commit reverted those changes for some reason.

-> e0d1b4b : added dataclass for modularised code.

-> 48bf1a6 & 5995c05 : removed timestamp and synchronised the cython stubs with code removing all the unnecassary errors.

-> cbee565 : pushed code to merge.

* `aiokafka/coordinator/`

-> added type-safety for all the files in coordinator.

**Implementation Approach:**
The implementation is just traditional linting check . All the type errors are resolved by using TypeIs middleware in some repos.

In many files, dataclass is used which returns more structured code, increasing readablity.

The implementation also involved carefully rewriting function definations and util files with type safety syntax.

**Potential Impact:**
This change impacts the readablity and future developer experience in this repo. By adding type safety probable clashes between services and type errors are resolved beforehand.

This might increase production efficiency and reputation of the repo as a quality repo, by using best practices.

---

### 2. Analysis of PR #115
**PR Summary:** This PR implements various validation checks and refactoring over existing fecther and producer service of kafka brokers. This PR also involve writing tests corresponding to fetcher and producer validation.

On many instances the refactoring of the fetcher included proper validation , using flexible type checks than existing rigid ones. Which was validated by the tests written in the test_fecther.py file.

Also many new test cases were written in the test_consumer.py file. Ensuring a robust system that passes every edge case.

**Technical Changes:**
* `/aiokafka/`
-> 57739c9 : refactoring of fetcher logic, in fetcher.py file. Replacing older offset checks with more robust and flexible checks, encompassing more test_cases.

Changing the _check_assignement var to check_assignement changing use policy from internal use to global use.

Also minor changes in comments in the producer.py file.

* `/aiokafka/test` 
-> 57739c9 : added test cases in test_consumer and test_fetcher files to test then freshly added validation checks, simulating the environment.

Also added global context manager to address to global variable and funcion defination.

* commit 64691e9 :
no major changes just changes in comments of fletcher.py file to match the context.

**Implementation Approach:**
Refactoring the fetcher and producer code such that it always calculated expected position as `current_msg.offset + 1`. This automatically handles compacted topics where offset might jump without the consumer hanging , fecthing for missing offset.

**Potential Impact:**
Increase the robusteness of the consumer, and make it resilient for unexpected inputs. This greatly effects the system reliablity and prevents consumer from hanging during service. This ensures that consumer not only reskonds when expected value is equal to offset but also when it is current offset + 1.
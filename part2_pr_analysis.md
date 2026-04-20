# Part 2: Pull Request Analysis

**Repository Selected:** `/aio-libs/aiokafka`

## Task 2.1: PR Selection and Comprehension

### PR Selection
I chose AIOkafka because the PRs looked familiar where there are typing changes, and also involved refactoring of existing codebase, something I am more confident about.

### 1. Analysis of PR #1006
**PR Summary:** The repo has already well-written code and all the unit tests were also written properly. This PR only added type safety ,and improves readablity of the code.

The codebase as appears to be is written using traditional / outdated coding syntaxes and appreoaches.This PR fixes all the errors and type errors in their `/records` and `/coordinator` sub-repos.

The syntaxes in many files don't match the syntax of modern Python dependencies and frameworks, thus this PR resolves all of the type errors , occured due to outdated techniques used previously by maintainers. Some minor feature additions were also there like use of TypeIS middleware. 

**Technical Changes:**
* `aiokafka/record/` 

• Added typing in the existing codebase, implemented cython functions for structured more modular code.(`094cb23 & 85a0415`)

• Fixed various type errors accross various files over the repo. (`b1efa77`)

• Implemented w/o protocol feature and in the next commit reverted those changes for some reason.(`7fa1efa & 58bc26c`)

• Added dataclass for modularised code.(`e0d1b4b`)

• Removed timestamp and synchronised the cython stubs with code removing all the unnecassary errors.(`48bf1a6 & 5995c05`)

• Pushed code to merge. (`cbee565`)

* `aiokafka/coordinator/`

• Added type-safety for all the files in coordinator.

**Implementation Approach:**
The implementation is just traditional static type analysis. All the type errors are resolved by using TypeIs middleware in some repos.

In many files, dataclass is used which returns more structured code, increasing readablity.

The implementation also involved carefully rewriting function definations and util files with type safety syntax.

**Potential Impact:**
This change impacts the readablity and future developer experience in this repo. By adding type safety probable clashes between services and type errors are resolved beforehand.

This might increase production efficiency and reputation of the repo as a quality repo, by using best practices.

---

### 2. Analysis of PR #115
**PR Summary:** The repo already has well-written code, and all the unit tests were properly implemented. This PR primarily adds type safety and improves code readability.

The codebase appears to be written using traditional or outdated coding syntaxes and approaches. This PR fixes all errors, including type errors, in the /records and /coordinator sub-repos.

Because the syntax in many files did not match modern dependencies, this PR resolves the type errors caused by redundant techniques previously used by the maintainers.
Some minor features were also added, such as the use of the TypeIs middleware.

The update also involves validation for the fetcher and producer services. By adding specific test cases to the consumer suite, the PR ensures the system remains stable across all partitions.

Instead of predicting the next offset based on an old state, the expected position is now dynamically calculated based only on the last successfully processed message

**Technical Changes:**
* `/aiokafka/`
• Refactoring fetcher logic, in fetcher.py file. Replacing older offset checks with more robust and flexible checks, encompassing more test_cases. (`57739c9`)

• Changing the _check_assignement var to check_assignement changing use policy from internal use to global use.

• Also minor changes in comments in the producer.py file.

* `/aiokafka/test` 
• Added test cases in test_consumer and test_fetcher files to test then freshly added validation checks, simulating the environment. (`57739c9`)

• Also added global context manager to address to global variable and funcion defination.

* commit 64691e9 :
• No major changes just changes in comments of fetcher.py file to match the context.

**Implementation Approach:**
Refactoring the fetcher and producer code such that it always calculated expected position as `current_msg.offset + 1`. This automatically handles compacted topics where offset might jump without the consumer hanging , fecthing for missing offset.

**Potential Impact:** Increase the robusteness of the consumer, and make it resilient for unexpected inputs. This greatly effects the system reliablity and prevents consumer from hanging during service. This ensures that consumer not only reskonds when expected value is equal to offset but also when it is `current offset + 1`. write this making minimal required changes and also rate that and try to keep it original.
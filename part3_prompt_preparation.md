# Part 3: Prompt Preparation

## Task 3.1: Comprehensive Prompt Documentation
**Selected PR:** PR #1006 (add typing to aiokafka/coordinator/*)

### 3.1.1 Repository Context 

`aiokafka/, aiokafka/record/ , aiokafka/coordinator/`

AioKafka is an asynchronous Python Client for Kafka built on top of asyncio framework. It is used to allow Python applications to communicate with Kafka brokers without blocking main execution thread.

The `/record` sub repo in aiokafka stores the code acting as a binary operation layer for the higher layers like producer and consumer. In layman language it holds the binary processing code in this subrepo.This is the repo which handles the `flow control` of the message streams. Chooses which protocol to follow also involves batch-building/framing of the data used by producer.It is also responsible for compression(gzip).

The `/coordinator` sub repo in aiokafka is the control-center for the consumer group. It manages python consumer and group coordinator (i.e kafka broker).It manages grouping , and also handles beats or sequencing of consumer groups. It is also responsible for the offset management service. One key feature involves error detection and triggers recovery logic.

While one repo signifies the binary processing or `low-level layer` the other is more of a control level layer on top of the other.

### 3.1.2 Pull Request Description
As the name suggest `add typing to aiokafka/coordinator/*` the PR implements typeing and type-safety in the existing codebase in the `records` and `coordinator` subrepos. The codebase is already well written but got some type errors and linting problems. Those were resolved by using the TypeIs middleware and type declarations in function definition. The PR involves refactoring of the codebase in some instances using `dataclass` which helps structure the object declaration properly, increasing developer experience and readablity of the code.

The PR consists of 12 commits mostly including refactoring original code and including type-safety in function decalrations. While the concerned sub-repos are `/record` and `/coordinator` repo under the `/aio-libs/aiokafka` tree.

The PR proposes changes in the `/record/_crecords/` , which includes addition of type-safety for existing functions. Also it replaces the old syntax used in `/records/default_records` with modern syntax supporting newer version of dependencies. This also creates a simplified version syncing cython based stubs with code.

Furthermore, the PR enhances the project's long-term maintainablity by aligning logic with modern asynchronous Python programming standards. The cleanup ensures that the future contributions to group management and binary level logic can be implemented with greater confidence.

The collective crux of the commits boil down to increasing type safety and refactoring existing codebase of both the subrepo components.

### 3.1.3 Acceptance Criteria

✓ Type-Safety compliance : The added code must pass through TypeIs validation, and the complete service must run without any significant errors.

✓ Cython Alignement : the binary layer must respond correctly to expected binary operations 

✓ Group Balancing : the `/coordinator` changes must be validated by a consumer balance check.

✓ Dataclass integrity : The refactoring must preserve the original function of the declared function

✓ Version compatiblity : the changes must be compatible with all the previous versions of Python, ensuring no 'module not found' error.

✓ When accessing message offsets and batch metadata, the system should provide full IDE support.


### 3.1.4 Edge Cases
1. **Spam Messages by user/ DDoS:** When a single user sends large number of messages and the batching layer is unable to group the batches properly.
2. **seek call during an active fetch call** This is the ultimate asynchronous test , the seek call must execute in parallel to an ongoing fetch call.
3. **Inconsistent type enforcements:** If no consistent type enforcements in cython extension files the they might break during runtime, causing the services to halt.
4. **Proper naming of variables:** Although obvious but if not catched during linting can cause some bugs in prodcution.

### 3.1.5 Initial Prompt
**Role:** You are an expert in Python Fundamentals, Distributed system, and related frameworks-Apache Kafka.

**Task:** 
 1. Typing(type-safety measures) 
 2. Refactor the current existing code according to updated types and software updates(if any)`.
 3. Check for any linting erros , check all the edge cases beforing finishing the submission.
 4. Check for the Repo context and the acceptance criterion.

**Context about the Repo:** 
Current directory: `@aiokafka/`

AioKafka is an asynchronous Python Client for Kafka built on top of asyncio framework. It is used to allow Python applications to communicate with Kafka brokers without blocking main execution thread.

The `/record` sub repo in aiokafka stores the code acting as a binary operation layer for the higher layers like producer and consumer. In layman language it holds the binary processing code in this subrepo.This is the repo which handles the `flow control` of the message streams. Chooses which protocol to follow also involves batch-building/framing of the data used by producer.It is also responsible for compression(gzip).

The `/coordinator` sub repo in aiokafka is the control-center for the consumer group. It manages python consumer and group coordinator (i.e kafka broker).It manages grouping , and also handles beats or sequencing of consumer groups. It is also responsible for the offset management service. One key feature involves error detection and triggers recovery logic.

While one repo signifies the binary processing or `low-level layer` the other is more of a control level layer on top of the other.

**Acceptance Criteria:**
✓ Type-Safety compliance : The added code must pass through TypeIs validation, and the complete service must run without any significant errors.

✓ Cython Alignement : the binary layer must respond correctly to expected binary operations 

✓ Group Balancing : the `/coordinator` changes must be validated by a consumer balance check.

✓ Dataclass integrity : The refactoring must preserve the original function of the declared function

✓ Version compatiblity : the changes must be compatible with all the previous versions of Python, ensuring no 'module not found' error.

✓ When accessing message offsets and batch metadata, the system should provide full IDE support.

**Testing Requirements:** 
- Integrate all new dataclass implementation in coordinator.
- You may use MyPy integration or other alternatives.
- Type guard verification using TypeIs middleware.
- Maintain consistency in cython validation.
- Make sure that the changes must support all the older versions.

**Edge Cases to Handle:**
1. Spam Messages by user/ DDoS: When a single user sends large number of messages and the batching layer is unable to group the batches properly.
2. seek call during an active fetch call This is the ultimate asynchronous test , the seek call must execute in parallel to an ongoing fetch call.
3. Inconsistent type enforcements: If no consistent type enforcements in cython extension files the they might break during runtime, causing the services to halt.
4. Proper naming of variables: Although obvious but if not catched during linting can cause some bugs in prodcution.


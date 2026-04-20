# Part 1: Repository Analysis

## Task 1.1 : Python-heavy repo selection

I checked for the tech-stack for each repo and this was the result:-
| Repository        | Percentage of Code Written in Python |
|------------------|--------------------------------------|
| AIOKafkaProducer | 93.1%                                |
| AirByte          | 48.2% (not python-heavy)             |
| ArchiveMaticha   | 83.1%                                |
| Beets            | 96.3%                                |
| MetaGPT          | 97.5%                                |


### Python-Primary Repository Analysis Table

All the data is refered from the respective documentation and docs of the repositories.

| Repository | Primary Purpose | Key Dependencies | Main Architecture Patterns | Target Domain |
| :--- | :--- | :--- | :--- | :--- |
| aio-libs/aiokafka | AIOKafkaConsumer is a high-level, asynchronous message consumer. It interacts with the assigned Kafka Group Coordinator node to allow multiple consumers to load balance consumption of topics (requires kafka >= 0.11). | asyncio, kafka-python, Docker, Cython, cram-jam  | Event-driven architecture, Pub/Sub pattern, Async I/O Loop | Distributed systems, Data streaming, Messaging, Networking |
| artefactual/archivematica | A comprehensive digital preservation system designed to maintain standards-based, long-term access to digital memory.Archivematica is a web- and standards-based, open-source application which allows your institution to preserve long-term access to trustworthy, authentic and reliable digital content. Our target users are archivists, librarians, and anyone working to preserve digital objects. | Django, Celery, MySQL/PostgreSQL | Microservices-oriented, Task Queue/Worker pattern, MVC (via Django) | Digital archiving, Institutional data preservation |
| beetbox/beets | The purpose of beets is to get your music collection right once and for all. It catalogs your collection, automatically improving its metadata as it goes. It then provides a suite of tools for manipulating and accessing your music. | mutagen, sqlite3, PyYAML | Plugin architecture, CLI-driven pipeline, Local DB caching | Media management, Consumer audio tooling |
| MetaGPT | Assign different roles to GPTs to form a collaborative entity for complex tasks. | pydantic, openai, asyncio, tenacity | Multi-Agent System (MAS), Message-passing, State Machine | Generative AI, Automated Software Engineering |
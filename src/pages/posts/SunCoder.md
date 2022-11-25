---
layout: "../../layouts/MarkdownLayout.astro"
title: "SunCoder"
subtitle: "An online programming platform."
url: "SunCoder"
pubDate: "25 Nov 2022"
---

During the past year I created an online programming platform that can be thought of as a mixture between edX and LeetCode.

My supervisors had the idea for a platform that first year students can learn to program on and that would automate marking of tutorials. This would save lecturers and tutorial assistents a lot of marking work.

## Tech Stack 🔥🔥🔥

I decided to use React for the front end and FastAPI for the back end. I settled on MariaDB for my database, and I used Docker to sandbox a remote code execution on the back end.

For a student to use the platform they would go to the online IDE in their browser. From the IDE they can perform remote code execution against a predefined set of test cases. When they test their solution their code is sent to the back end and a Docker container executes the code in a sandboxed environment. This prevents malicious code from compromising the system.

## Issues early on 🙃

Early on scalability was an issue as I was creating a new Docker container for each remote code execution. The Docker daemon is also synchronous which causes all containers to start one after the other. Docker containers took 500ms to startup on average on my system (M1 macbook air 2020) which meant that running 10 remote code executions would take 5 seconds. Was not acceptable from a scalability perspective as the system was being built for 500 students.

Another issue that I faced was managing the highly relational data. There were self-referencing many-to-many relationships, triple join on many-to-many tables, and 6-level deep nested relationships just to mention a few of the complex relationships that existed in the data.

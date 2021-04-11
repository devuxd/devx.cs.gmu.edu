---
layout: project
title: Microtask Programming
youtube_video: https://www.youtube.com/watch?v=mIn2EOqsDYw
# photo: 
short_desc: Onboarding on a new project is often a long, hard process, dissuading casual contributors from ever starting. What if you could contribute code to a new software project in a few minutes? How would enabling many transient contributors change software development? We've been exploring these questions through building web-based programming environments which enable microtask programming and conducting studies to understand how they change software development work.
current_collaborators: [Emad]
prev_collaborators: [Ankit, Aarushi]
active: true
---
What if you could contribute code to a new software project in a few minutes? How would enabling many transient contributors change software development?

In microtask programming, developers complete short self-contained microtasks through the use of 
a specialized programming environment. Given only a textual description of the purpose of a function and its implementation, 
a developer might be asked to identify, test, and implement a new behavior. To complete larger programming tasks, microtasks may 
be automatically generated and aggregated. 
Microtask programming is envisioned to offer a number of benefits, including reduced time onboarding developers onto a project and 
faster time-to-market through greater parallelism.

Key to the effectiveness of crowdsourcing approaches for software engineering is workflow design,
describing how complex work is organized into small, relatively independent microtasks. In this paper, we introduce a Behavior-Driven Development (BDD) workflow for accomplishing programming
work through self-contained microtasks, implemented as a preconfigured environment called Crowd
Microservices. In our approach, a client, acting on behalf of a software team, describes a microservice
as a set of endpoints with paths, requests, and responses. A crowd then implements the endpoints,
identifying individual endpoint behaviors which they test, implement, and debug, creating new functions and interacting with persistence APIs as needed. To evaluate our approach, we conducted a
feasibility study in which a small crowd worked to implement a small ToDo microservice. The crowd
created an implementation with only four defects, completing 350 microtasks and implementing 13
functions. We discuss the implications of these findings for incorporating crowdsourced programming
contributions into traditional software projects.
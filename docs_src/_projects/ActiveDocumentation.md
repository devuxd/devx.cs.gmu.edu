---
layout: project
title: Active Documentation
# youtube_video: 
photo: /assets/img/research/ActiveDocumentation.png  
short_desc: In Active Documentation, we explore approaches to help developers easily document, check, and update design rules in code.
current_collaborators: [Sahar]
prev_collaborators: [Gennie, Ayesha, Aarav, Emily, Rahul]
active: true
---

## ActiveDocumentation

Good documentation has long been argued to be key to helping developers write code more quickly and 
consistently with design decisions, but is left largely disconnected from code. 
We propose a method for active documentation, where design decisions are made explicit as 
design rules and checked against code. Developers can discover how to follow a design rule 
by navigating to examples in their codebase. After editing code, developers receive immediate 
feedback about which design rules are satisfied and which are violated, notifying developers who miss 
design decisions about the existence of these design decisions.

<iframe width="560" height="315" src="https://www.youtube.com/embed/_AT8sNj02Ss" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## RulePad


Developers have long been encouraged to use documentation to learn about software design 
and make sure the code changes are consistent with the documentation.
However, this does not happen. The reason is that documentation and code are disconnected.
Using Active Documentation, design rules in documentation are formulated as checkable constraints.
But existing tools do not offer enough support. 
In RulePad, we propose new techniques for authoring checkable design rules.

You can learn more [here]({{ site.baseurl }}{% link _tools/RulePad.md %}).
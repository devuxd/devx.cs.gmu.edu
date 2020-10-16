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


Good documentation offers the promise of enabling developers to easily understand design decisions. 
Unfortunately, in practice, design documents are often rarely updated, becoming inaccurate, incomplete, and untrustworthy. A better solution is to enable developers to write down design rules which may be checked against code for consistency. But existing rule checkers require learning specialized query languages or program analysis frameworks, offering a barrier to writing project-specific rules. 
We introduce two new authoring techniques for design rules: snippet-based authoring and semi-natural-language authoring.
In snippet-based authoring, 
developers specify characteristics of elements to match by writing partial code snippets. 
In semi-natural language authoring, 
a textual representation offers a representation for understanding design rules and resolving ambiguities, 
which is bidirectionally synchronized.  
We implemented these approaches in RulePad. 
See the demo of this tool [here]({{ site.baseurl }}{% link _tools/RulePad.md %}).


<iframe width="560" height="315" src="https://www.youtube.com/embed/u_IjorRovxc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
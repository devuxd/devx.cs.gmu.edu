---
layout: tools
key: RulePad
title: RulePad
youtube_video: https://www.youtube.com/watch?v=dQHbItcr2Aw
# photo:
short_desc: Good documentation offers the promise of enabling developers to easily understand design decisions. Unfortunately, in practice, design documents are often rarely updated, becoming inaccurate, incomplete, and untrustworthy. A better solution is to enable developers to write down design rules which may be checked against code for consistency. But existing rule checkers require learning specialized query languages or program analysis frameworks, offering a barrier to writing project-specific rules. We introduce two new authoring techniques for design rules; snippet-based authoring and semi-natural-language authoring. We implemented these approaches in RulePad. 
papers: [Mehrpour2020RulePad]
---

RulePad is a part of [Active Documentation]({{ site.baseurl }}{% link _projects/ActiveDocumentation.md %}) project.

Good documentation offers the promise of enabling developers to easily understand design decisions. 
Unfortunately, in practice, design documents are often rarely updated, becoming inaccurate, incomplete, and untrustworthy. A better solution is to enable developers to write down design rules which may be checked against code for consistency. But existing rule checkers require learning specialized query languages or program analysis frameworks, offering a barrier to writing project-specific rules. 
We introduce two new authoring techniques for design rules: snippet-based authoring and semi-natural-language authoring.
In snippet-based authoring, 
developers specify characteristics of elements to match by writing partial code snippets. 
In semi-natural language authoring, 
a textual representation offers a representation for understanding design rules and resolving ambiguities, 
which is bidirectionally synchronized.  
We implemented these approaches in RulePad. 


Our paper is published and presented in ESEC/FSE 2020. 

#### 2-Minute Teaser

<div class="youTube-wrapper mt-3 mb-5">
<iframe width="560" height="315" src="https://www.youtube.com/embed/dQHbItcr2Aw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

#### Full Presentation

<div class="youTube-wrapper mt-3 mb-5">
<iframe width="560" height="315" src="https://www.youtube.com/embed/4rUYS8enKA0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>


### Tool Demo 

RulePad is implemented as a plugin for IntelliJ IDE. 
The following demo is a partial implementation of RulePad. Some of RulePad features require IDE APIs, and thus is not available in the online Demo. 
You can checkout the complete behavior of RulePad [here](https://www.youtube.com/watch?v=u_IjorRovxc).

<div style="overflow: auto">
<iframe height="810" width="1000" src="https://saharmehrpour.github.io/RulePad-Demo/"></iframe>
</div>
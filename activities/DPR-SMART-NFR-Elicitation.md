---
Scope: Entire system, individual parts
Phases: "Analysis"
Roles: "Application architects, other architects"
Input: "Project goals, functional requirements"
Output: "NFR document, formal or informal"
Abstraction/Refinement Level: all
---


Activity: *SMART NFR Elicitation*
---------------------------------

<!-- TODO (v2) decide on split: "Group NFRs by Type" or "select taxonomy" could be a separate activity that features FURPS, etc.; activity vs. artifact? -->

### Context
*Non-Functional Requirements (NFRs)*, including *Quality Attribute (QAs)*, describe *how* a system provides its functionality, not what it does (which is the purpose of functional requirements specifications such as [user stories](../artifact-templates/DPR-UserStory.md) or [use cases](../artifact-templates/DPR-UseCase.md)). Examples of key QAs are reliability, usability, efficiency (e.g., performance, scalability), maintainability, and portability according to [ISO/IEC standard 9126](https://en.wikipedia.org/wiki/ISO/IEC_9126). ISO 9126, now superseded by a newer standard, also lists functionality as a quality category.

Note that while common, the term and acronym NFR are not received well by some thought leaders and practitioners; they prefer terms such as "extra-functional". Not all non- or extra-functional requirements qualify as quality attributes, as there are organizational and educational constraints as well; hence, an extra term is needed. We decided for NFR here, weighting popularity higher than accuracy (to express our decision in terms of desired qualities).


### Goal and Purpose (When to Use and When not to Use)
Expressive, unambiguous NFRs that find their way into project plans and the minds of the project participants are the main output of architectural analysis. Without such NFRs, architecture design work becomes a blind flight; the project team is at the mercy of the client or internal project sponsor who can come up with new and more advanced requirements as they wish.

Practical challenges of NFR elicitation include:

* Many QAs are exist and usually the project budgets do not allow to specify all of them precisely. Furthermore, many conflicts between them exist (for instance, implementing a security feature has a performance cost); a prioritization is required, but hard to commit to and agree upon (for many stakeholders). 
* QAs are often stated on inadequate level of abstraction, for instance per system and not per logical function or business process step. They keep on changing.
* Many attributes are hard to quantify. Hence, QAs often remain under-specified (so they are unknown and cannot serve as the base of design decisions and acceptance tests) or are over-specified (and therefore overly ambitious and hard to meet).

Therefore, it is desirable to establish criteria and templates that allow architects and other participants in architectural analysis to overcome these challenge so that NFR elicitation and architectural analysis become effective and efficient.

<!-- Source: https://miro.com/app/board/o9J_kmuX5tA=/?fromEmbed=1 -->
<img src="images/DPR-NFRElicitation.png" height="400" />

### Instructions (Synopsis, Definition)
*Select and apply a taxonomy consistently.* There are many different NFRs, Quality Attributes (QAs) in particular. Many of these pertain to the runtime, others deal with software support and maintenance. Therefore, many attempts have been made to organize the QA landscape (ordered from informal and ad hoc to formal and complete): 

* The basic, easy-to-remember *FURPS+* classification introduced in the lecture and used in exercise 1, originally introduced in a software engineering book from the 1990s and explained in [this article by P. Eeles](https://www.ibm.com/developerworks/rational/library/4706.html).
* ISO 9126 and its successor [ISO 25010](http://iso25000.com/index.php/en/iso-25000-standards/iso-25010), also used by in "Effektive Softarearchitekturen" @Starke:2015 and recommended for use in arc42 descriptions.
* SEI quality utility trees, see this Technical Report, [this article](http://arnon.me/2010/05/utility-trees-hatching-quality-attributes/) by Arnon Rotem-Gal-Oz and [arc42 tip 10-2](http://docs.arc42.org/tips/10-2/).

*Be SMART*. [*SMART criteria*](https://en.wikipedia.org/wiki/SMART_criteria) are frequently used in project and people management. All five letters can have different meanings<!--(is this an instance of "semantic diffusion"?-->; here, we use these meanings: *S* for specific, *M* for measurable, *A* for agreed upon, *R* for realistic, and *T* for time-bound.

The SMART criteria can be applied to NFR elicitation in a straightforward way and therefore serve as "meta-qualities" (quality attributes of/for quality attributes, that is):

* S: Which feature or part of the system (or the build-time process and supporting infrastructure) should satisfy the requirement? Which type of environment does the requirement pertain to (for instance, normal operations a.k.a. "sunny day", peak loads, error situations)? 
* M: How can testers and other stakeholders find out whether the requirement is met (or not)? Is the requirement quantified?
* A: Do all affected internal and external stakeholders agree on the 'S' and the 'M' wording? (issue for requirements engineering and project management, so out of scope here and now)
* R: Is it technically and economically feasible to achieve the 'M' measure in the context of all features or system parts specified under 'S'? (issue for requirements engineering and project management, so out of scope here and now)
* T: When should the NFR meet the 'M' measure, is there a growth path from iteration to iteration? (also to be answered by project management, so out of scope here and now)

S is about *scoping* the requirement (note that the word “specific” might suggest a different meaning, possibly similar to "M"?). 

> Which functional requirement or part of the design/system under construction requires the specified quality property? 

Not all features need the same (high) availability 
E.g. end user causing revenue vs. monthly master data update. And not all quality are as cross cutting as security. And even security sub-requirements might differ per data element/per user story/per component.

M is about *monitoring* the requirement throughout a project. You should be able to answer/assess: 

> Is the NFR achieved or not? 

Explanations (excuses?) for not coming up with numbers are easy to find (e.g., fear of over-commitment might cause under-specification), but will get to you in the long run (project example given in the lecture: “standards compliance (past, present and future)”, "flexible data model", "scale console").

<!-- TODO (v2) also document A, R, T on level of detail of S and M? -->

SMARTness assessments can be recorded in the following way: 

| ASR | Specific (Y/N)? | Measurable (Y/N)? | Rationale for Answers | Improvement (if needed) |
|:----|:----------------|:------------------|-----------------------|-------------------------| 
| R1 | [Y/N] | [Y/N] | (answer to question from above) | (required change or n/a) | 
| Rn | [Y/N] | [Y/N] | ... | ... | 

<!-- Another "meta quality scheme" is CARGO (for decisions and designs):
* C - changeable (no dead ends)
* A - aesthetic
* R - reproducible/repeatable ("nachbaubar")
* G - good enough (simple, lean)
* O - observable 
(source: ZIO) -->

*Prioritize by effort, benefit, risk*. See this [IEEE Software article](https://www.zora.uzh.ch/id/eprint/7375/).


### Example(s)
An example and a counter example are (which one is SMARTer than the other?): 

* "The system should be highly usable, perform well and easy to maintain."
* "The ‘place order’ user story must complete in less than a second."

In a telecommunications order management system, requirements that deal with external and internal quality properties may be:

* *Accuracy*: orders must not be lost, resource reservations must be undone
* *Efficiency* (here: performance): sub-second response times specified
* *Interoperability*: multiple platforms to be supported
* *Modifiability*: skills for selected technologies must be available locally

An example of a constraint is "only relational database management system X can be used because an enterprise-wide licensing agreement is in place and the required database administration skills have been built up". 

*Availability* is another example of an important NFR. A system is available if it is up and running and produces correct results (or: a system fails if it gives a wrong answer or no answer at all)
The availability of a system is the fraction of time it is available. A system is highly available if its availability is close to 1. Thus, high availability is the property of a system to be up and running all the time, always producing correct results. Hence, the (in)famous availability requirement is... “24x7”. True high availability is expensive to achieve (think about maintenance intervals, need for fault-tolerant hardware, etc.).

The more a system fails, the less it is available; the longer it takes to repair a system after it fails, the less it is available. Systems that depend on others “inherit” their availability partly.
 “Mission-critical” middleware such as database management systems, transaction processing monitors, workflow management systems must be highly available – so that supported applications can meet their NFRs.


### Benefits vs. Effort (Expected Benefits, Skill Levels)
See this [IEEE Software article](https://www.zora.uzh.ch/id/eprint/7375/) for guidelines when to invest in deep and SMART NFR elicitation, and when not to.


### Hints and Pitfalls to Avoid (Common Pitfalls)

* State assumptions if stakeholder input is incomplete or insufficient; have these assumptions reviewed and approved.
* Define [landing zones](http://wirfs-brock.com/blog/2011/07/28/agile-landing-zones/) if single numbers are hard to come up with and agree upon.
* Be assertive in your [technical writing](https://ozimmer.ch/tags/#technical-writing); avoid filler words such as "in principle" , "generally", "more or less", etc. 
* Make conflicts between NFRs explicit, prioritize and find tradeoffs. For instance, balance security and performance requirements.
* Do not hesitate to refined or relax NFRs as the system evolves and you learn more about actual user wants and needs and technical feasibility of runtime qualities.

The [arc42 website](https://docs.arc42.org/section-10/) provides eight more hints.


### Origins and Signs of Use
NFRs and quality management have been a key theme in software engineering since the very beginnings 50+ years ago. Words ending with "-ility" often indicate NFR awareness and analysis.

Numbers usually indicate that the 'M' property has been strived for; explicit mention of the system under construction and/or individual use cases/user stories and system components indicates the 'S' in SMART. 


### Related Content

#### Performing Roles and Related Artifacts (Synopsis)

* [Application Architect](../roles/ApplicationArchitect.md) and other decision makers

<!--
|**Role**| Input | Output | Comments |
|:-|:-----:|:------:|:--------:|
|  |  |  |  |
-->

#### Practices and Techniques (Refinements, Guides)

* Quality Attribute Scenarios (QAS) and utility trees (SEI) @Bass:2012
* [Mini-Quality Attribute Workshop (QAW)](https://www.neverletdown.net/p/mini-quality-attribute-workshop.html), a simplified form of the QAWs that are part of the Architecture Tradeoff Analysis Method (ATAM) @Barbacci:2002.
* [Quality storming](https://speakerdeck.com/mploed/quality-storming)


### More Information 
arc42 recommends to have [top three to five QAs in Section 1 of architecture descriptions](http://docs.arc42.org/section-1/), suggests a [Section 2 dealing with constraints](http://docs.arc42.org/section-2/) and puts the detailed quality requirements section towards the end in [Section 10](http://docs.arc42.org/section-10/).

Websites dedicated to software quality include [Quality-Aware development](http://www.quality-aware.com/).


### Data Provenance 

```yaml
title: "Design Practice Repository (DPR): SMART NFR Elicitation"
author: Olaf Zimmermann (ZIO)
date: "08, 14, 2020 (Source: Project DD-DSE)"
copyright: Olaf Zimmermann, 2020 (unless noted otherwise). All rights reserved.
license: Creative Commons Attribution 4.0 International License
```

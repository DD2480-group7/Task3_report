# Report for assignment 3
This is a template for your report. You are free to modify it as needed.
It is not required to use markdown for your report either, but the report
has to be delivered in a standard, cross-platform format.

## Project
Name: Zulip
URL: https://github.com/zulip/zulip

Zulip is an open source team chat combining the immediacy of slack with an email threading model.

## Architectural overview (optional, as one item for P+)

## Selected issue(s)
Title: Clean up email_mirror code. #1836
URL: https://github.com/zulip/zulip/issues/1836

Three methods were moved out of actions.py into lib/email_mirror.py. get_email_gateway_message_string_from_address was made to throw an exception if it can't find an email.

## Onboarding experience
1.  Did it build as documented?
(See the assignment for details; if everything works out of the box,
there is no need to write much here.)

The onboarding experience as a windows user for the zulip-project was complicated and time-demanding since the current setup for windows is flawed and the documentation offered no support for the issue. 
Two team members using windows had the issue of the Vagrantfile on line 35 checking the version of lxc-ls. Our guess is that the Vagrantfile isn’t supposed to be run for windows users.
To find the solution the “Troubleshooting and Common Errors” and “#provision help”-channel in zulip was studied, Git-BASH and Python was re-installed, the repo was re-cloned and windows permission-errors was examined.
Docker was also used to try to replace Vagrant but Docker required Windows Pro while the user had Windows Home.
The issue was finally resolved by one user commenting out line 35 and hard-coding the variable LXC_VERSION to 2.1.0. We have no confirmation of whether the zulip-team accepts this solution.    


## Requirements affected by functionality being refactored

### Req3:
Requirements related to the functionality tageted by the refactoring: 
(identified (by name(ID), title and description, and other optional attributes) and described in a systematic way)

## Existing test cases relating to refactored code

## The refactoring carried out
(Link to) a UML diagram and its description

### Req7:
Key features affected by the refactoring are shown in UML class diagrams (before/after).
Note: you do not have to show classes, fields, or methods that are not changed, unless they help with the overall understanding.

## Test logs
Overall results with link to a copy of the logs (before/after 
refactoring).
The refactoring itself is documented by the git log.

### Req5:
Changes to the test suite are shown and documented, e.g. as a patch

## Effort spent
For each team member, how much time was spent in
1.  plenary discussions/meetings;
2.  discussions within parts of the group;
3.  reading documentation;
4.  configuration;
5.  analyzing code/output;
6.  writing documentation;
7.  writing code;
8.  running code?

## Overall experience
What are your main take-aways from this project? What did you learn?
Is there something special you want to mention here?

The main take-aways for this project are an insight into the complexity of refactoring in a real-world open-source project.
Even if the given documentation/examples of the project were quite extensive, some members still experienced issues with the onboarding experience. 
The community of the project seems to be fairly active, with contributers posting not only on the github issues but also daily in zulip channels like "#provision help". Our team even got the opportunity to post about our onboarding issues in this channel and potentially help future contributors. 

### Req8:
The overall work carried out, and experience gained, are documented. In particular, mention your experience about 

the given documentation/examples of the project, 
its tool framework, 
and the interaction within your team and with the community of the project.

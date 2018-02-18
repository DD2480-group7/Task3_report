# Report for assignment 3
This is a template for your report. You are free to modify it as needed.
It is not required to use markdown for your report either, but the report
has to be delivered in a standard, cross-platform format.

## Project
Name:
URL:
One or two sentences describing it

## Architectural overview (optional, as one item for P+)

## Selected issue(s)
Title:
URL:
Summary in one or two sentences

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

## Existing test cases relating to refactored code

## The refactoring carried out
(Link to) a UML diagram and its description

## Test logs
Overall results with link to a copy of the logs (before/after 
refactoring).
The refactoring itself is documented by the git log.

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

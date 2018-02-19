# Report for assignment 3

## Project
* Name: Zulip
* URL: https://github.com/zulip/zulip
* Basically Slack but open source and with a email threading model. (Also LaTeX inline-support :heart:!)


## Architectural overview
![Components](architecture_simple.png)
## Selected issue(s)
* Title: Clean up email_mirror code
* URL: https://github.com/zulip/zulip/issues/1836
* The issue entailed moving a couple of methods and changing so that when an error occured the method cast an exceptions instead of returning `None`. The changes, thus, also required modifications in calling methods in order to catch the error that was cast.

## Onboarding experience
Zulip is a very well documented project with a great community with helpful people.

To help with onboarding they have a ["Contributing to Zulip, getting started"-guide](https://zulip.readthedocs.io/en/latest/overview/contributing.html). The documentation contains everything from how to set up a development environment to how to run tests, what tests correspond to what parts of the code, code standards and extensive documentation for the different parts of the code. The prerequisite tools for the project were Git, Git for Windows (for windows users) Vagrant, Virtualbox, vagrant-lxc plugin (for linux users). The tools were well documented in the getting started-guide. Unfortunately there were errors depending on what operating system the contributor was using that the documentation had no answers to. When running “vagrant up” Vagrant downloaded the base Ubuntu 14.04 virtual machine image (for macOS and Windows) or container (for Ubuntu), configured this virtual machine/container for use with Zulip, created a shared directory mapping the clone of the Zulip code inside the virtual machine/container at ~/zulip and ran the tools/provision script inside the virtual machine/container, which downloads all required dependencies, sets up the python environment for the Zulip development server, and initializes a default test database. A [log](provision.log) from provisioning is included in this repository.

The onboarding experience as a windows user for the zulip-project was complicated and time-demanding since the current setup for windows is flawed and the documentation offered no support for the issue.
Two team members using windows had the issue of the Vagrantfile on line 35 checking the version of lxc-ls. Our guess is that the Vagrantfile isn’t supposed to be run for windows users.
To find the solution the “Troubleshooting and Common Errors” and “#provision help”-channel in zulip was studied, Git-BASH and Python was re-installed, the repo was re-cloned and windows permission-errors was examined.
Docker was also used to try to replace Vagrant but Docker required Windows Pro while the user had Windows Home.
The issue was finally resolved by one user commenting out line 35 and hard-coding the variable LXC_VERSION to 2.1.0. We have no confirmation of whether the zulip-team accepts this solution. 

For Mac users the experience of downloading and setting up the above mentioned tools was easy, and one could follow the guide step by step.  

For communications Zulip uses their own platform where they have a community server set up and where there always is someone that's able to help if you're stuck or having problems. We have used this a bit in order to get clarifications.

All in all this gives a very good base for great onboarding. It also sets a high standard for us as coders to follow the specified coding style and principles.

### Third party services (mentioned in subsystems documentation): 
* PostgreSQL
  * Database for persistent data
* Redis
  * Used for short-term data stores
* Nginx
  * Front end web-server 
* RabbitMQ
  * Queuing system.
* Django & Tornado
  * Django: main web application server
  * Tornado: runs server to client real time push system
* HTML templates
  * Jinja 2: backend templates
  * Handlebars: frontend templates
* Supervisor
  * Starts and restarts server processes automatically if they crash.
* Memcached
  * Used to cache database model objects
* Nagios
  * Used for notifications to the system
  
## Requirements affected by functionality being refactored
#### 1 - Location of methods get_email_gateway_message_string_from_address, encode_email_address_helper, decode_email_address
These three methods should be moved from zerver/lib/actions.py to zerver/lib/email_mirror.py.

#### 2 - Dependencies are correct
After moving the three methods (see Requirement 1) we have to make sure dependencies are correct; that is, import statements have been changed according to the relocation and calling methods work as before. All tests should pass for the project.

#### 3 - get_email_gateway_message_string_from_address should throw ZulipEmailUnrecognizedAddressError
Earlier get_email_gateway_message_string_from_address returned None if the email address submitted did not match the specified regex pattern. Now the method get_email_gateway_message_string_from_address should raise an exception instead. All calling methods should handle this so that the overall functionality of the code remains the same and all tests should pass for the project.

#### 4 - Add tests to test functionality of exception-throwing in get_email_gateway_message_string_from_address
We have to make sure that an exception is thrown when no match is found for submitted email address, and that the method terminates as it should when a match is found. To fulfill this we need at least two tests: one positive and one negative. All tests (including our new ones) should pass.

### Req3:
*Requirements related to the functionality tageted by the refactoring:
(identified (by name(ID), title and description, and other optional attributes) and described in a systematic way)*

## Existing test cases relating to refactored code
When it comes to this refactoring problem it was important that all tests that existed when we started working on the code would still pass after our changes had been made. This meant that we had to make sure all dependencies were correct and that calling methods could handle the exception being raised. If we succeeded in this all existing test cases should pass just as before.

We focused on the tests in the test file zerver/tests/test_email_mirror.py since it was the file that tested the functionality of email_mirror.py. Even though the project states that they have a high code coverage, the tests are quite large; that is, they test different situations that can occur from a higher level rather than testing all the different cases of each method. Therefore, we kept these methods as they were, assuming that they covered what zulip considered important cases, and made sure that they still passed after the refactoring had been implemented. Using the UML we had quite a good overview of what methods were affected by our refactoring and how they were tested.

## The refactoring carried out
The following is a simplified UML-diagram over the classes and methods before and after they were affected by our refactoring. 

Since the affected classes are very large, fields and other unnessecary data has been omitted to give a clearer overview over what's been changed and how it affects each method. 

An asterix (*) after the method name implies that the specific method is called from a test case. 


![Components](zulip_diagram.png)

## Test logs
Overall results with link to a copy of the logs (before/after
refactoring).
The refactoring itself is documented by the git log.

### Req5:
*Changes to the test suite are shown and documented, e.g. as a patch*

## Effort spent

*Alexander Manske*
1.  plenary discussions/meetings;
2.  discussions within parts of the group;
3.  reading documentation;
4.  configuration;
5.  analyzing code/output;
6.  writing documentation;
7.  writing code;
8.  running code?

*Alexander Viklund*
1.  plenary discussions/meetings;
2.  discussions within parts of the group;
3.  reading documentation;
4.  configuration;
5.  analyzing code/output;
6.  writing documentation;
7.  writing code;
8.  running code?

*Alfrida Mattisson*
1.  plenary discussions/meetings ≈ 2
2.  discussions within parts of the group ≈ 2
3.  reading documentation ≈ 5
4.  configuration ≈ 1
5.  analyzing code/output ≈ 4
6.  writing documentation ≈ 7
7.  writing code ≈ 8
8.  running code ≈ 1

*Hanna Nyblom*
1.  plenary discussions/meetings;
2.  discussions within parts of the group;
3.  reading documentation;
4.  configuration;
5.  analyzing code/output;
6.  writing documentation;
7.  writing code;
8.  running code?

*Lukas Szerszen*
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
The community of the project seems to be fairly active, with contributers posting not only on the github issues but also daily in zulip channels like "#provision help". Our team even got the opportunity to post about our onboarding issues in this channel and potentially help future contributors. It was also interesting to see how the project was almost like a company with guides for almost everything imagineable and, for example, a code of conduct. Whatever you could think of, be it mocking tests, importing libraries or writing commit messages, there was a guide for it.

### Req8:
*The overall work carried out, and experience gained, are documented. In particular, mention your experience about
the given documentation/examples of the project,
its tool framework,
and the interaction within your team and with the community of the project.*

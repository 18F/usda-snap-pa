# Preliminary Evaluation v1.0 SWIM Code Deliverables
5.4.18

## The following code deliverables are evaluated in this document:
- swim-alfresco-repo-uatrelease2.3.1/
- swim-alfresco-share-uatrelease2.3.1/
- swim-jq-uatrelease2.3.1/)

## Evaluation Overview
Below is a preliminary evaluation of the code developed for the SWIM application before April 2018. This evaluation considers code written for the front end of the application as well as that written for the back end. **Note that this is an initial draft that we are distributing for feedback. We anticipate that it will be a conversation starter, and that changes and additions will be made before our final draft.**

In this preliminary evaluation, we focused on four criteria to consider whether the code would be salvageable and reusable by other developers: 
- (1) understandability, 
- (2) documentation, 
- (3) buildability, and 
- (4) interoperability. 

## Explanation of Criteria Used
### Understandability
We took into consideration how easy it would be for a new developer to begin to work with these different codebases. We recognize that there will always be a margin of chaos for someone picking up with an existing codebase. That said, there are some factors that make it easier for a new person to get up to speed. Some of the factors that we believe make code understandable are:
- whether the code came with comments intended to onboard a new team member;
- whether the code was written clearly, simply, and without redundancies;
- how modular the code is; and  
- whether there are functioning tests provided for the codebase (this is very important!);
### Documentation
We took into consideration the amount of materials provided by the previous team to assist a new team with onboarding. Documentation is the backbone of any codebase and is required reading for any engineer that attempts to maintain and operate it. Without documentation of how the code functions, an engineer inevitably engages in a lot of guesswork in order to utilize the code. Poor documentation can lead to inefficient onboarding. 
Note that part of writing strong documentation is including references to existing documentation that is relevant. For example, when code follows a popular framework, its documentation, at a minimum, should say so and should reference the well-known instructions from that framework.
### Buildability
We took into consideration the speed and ease at which a new team would be able to take the source code and deploy, or run, it. In the case of SWIM, we measured this by looking at how the SWIM Alfresco Repo, SWIM Alfresco Share, and SWIM JQ projects would need to be compiled and built in order to reach in a functional state. Because there are three codebases the buildability for this project is highly complex. Also, the buildability varies across the individual projects as well due to the nature of the codebases.
### Interoperability
We took into consideration how well the pieces of software interact with and depend on one another and their target framework. More dependencies means more need for refactoring to accommodate re-writing the dependency. When there is a high amount of refactoring required, salvaging existing code might not be worth the effort. 

## Evaluation Summary (Preliminary)
Our recommendation based on the discussed criteria is that:
- Regarding the backend, the Alfresco Repo and Alfresco Share code do not seem salvageable in their current state. They require significant refactors around documentation, and tests.
- Regarding the front end, the Alfresco JQ code interaction code seems like it could be salvageable. 
- We would want to weigh other available options before concluding that salvaging the Alfresco JQ code would be the most efficient and cost effective option.

## SWIM Alfresco Repo UAT Release 2.3.1
### Preliminary Summary
This is the AMP Alfresco Repo project. This code contains the backend for the Alfresco Application Module Package (AMP), which communicates with the main Alfresco Repository.  The codebase is built for the Alfresco framework. 
This code would only be salvageable if Alfresco remains the target platform. Some of the code is incomplete and contains failing tests. There are many times in this codebase where the functionality is left to be interpreted by a team member with high contextual information of the project. Without that contextual knowledge, this codebase cannot be salvaged. 
### Understandability
The code’s understandability is low. With almost all of the comments in the code being reused as either placeholder or generic comments that don’t actually provide any context into what the code is doing. Comments in the codebase are duplicated, which makes them confusing to follow.
The logic expressions in the code are difficult to understand as they span hundreds of columns checking for multiple conditions to be true or false and also meet other true or false conditions. These logic expressions need to be either better documented when they occur or consist of variable names that express their intentions.
Because of the lack of documentation (more on that below), this codebase is very difficult to understand without contextual knowledge of the application as a whole. 
### Documentation
There are some major inconsistencies with how the project is setup based on the documentation provided. Many times the documentation needed to be rewritten in order to get the code to properly run. Some documentation for this project exists, but even with it, we had to do a lot of work to get it into a functional state. There was missing contextual information and missing commands that were not provided in the codebase and needed troubleshooting to get them operational again.
Documentation was missing to explain what each method or feature does. Also, we found documentation copied and pasted across multiple different files, which was confusing to read because the comments did not seem to have broad applicability that would be appropriate in all of these different places (see the screenshot on the right for an example of repeated documentation which is only correct in one of the instances it appears in). Notice that serial number only exists in the bottom HTTP method call but is incorrectly referenced in the top HTTP method call’s comments.
### Buildability
Builds for this AMP package are repeatable once the issues around documentation were addressed.
### Interoperability
This codebase is interoperable with the Alfresco JQ project (it can interact with it) although it is incomplete. Though aspects of the codebase can be reused, in order to do this, the codebase would need to be better documented, have more tests written, and be refactored to remove extraneous comments and unused code blocks.

## SWIM Alfresco Share UAT Release 2.3.1
### Preliminary Summary
This codebase consists mainly of static images and examples extracted from the Alfresco Share UI tutorial. It contains no additional functionality built on top of Alfresco. This could be reused.
### Understandability
This is the Alfresco Share UI project. This codebase is almost completely comprised of the tutorial for building an Alfresco Share UI project with very little customization. The only customization here is the file found in src/main/amp/web/gov/usda/fns/swim/assets/html/index.html. This leads me to understand that this codebase is almost entirely incomplete or at least disorganized enough to cause confusion with other developers taking on this work.
### Documentation
The documentation in this project doesn’t address what the functionality of the Share UI is. The README.md file states that the Share UI module serves the static assets such as images and CSS for the SWIM email notifications. The problem with this explanation is that the images directory is the only directory that contains customized images for the SWIM application. The documentation in this project does not address how to properly build this project for use in a production or development environment.
### Buildability
There is a run.sh and run.bat file in this project. This properly addresses how to get the project running, but does not explain how to build the project in a .war ([Java] Web ARchive) file. There is no clear documentation or information about how to continually build the project included in the repository. This leads developers to rely on Alfresco framework knowledge or documentation to figure it out.
### Interoperability
This codebase is interoperable with other projects and does not pose dependency risks since all it contains are static images in the src/main/amp/web/gov/usda/fns/swim/assets/images/ path.

## SWIM JQ UAT Release 2.3.1
### Preliminary Summary
This codebase consists of the JavaScript Angular code. This codebase is salvageable only from the perspective that it contains some useful code for the various interactions on the front-end, but it requires a significant refactor for how it communicates with the backend servers.
### Understandability
This code is poorly organized but has well commented in certain important files. The code is repetitive in some places with duplicate functionality in various method calls. I recommend that this code be refactored. It’s refactoring would need to take into account both removing repetitive methods from the codebase and interacting with a different backend. Thankfully most of this work is contained to a single file swim-jq-uatrelease2.3.1/assets/js/swim-1.0.js.
This project is entirely comprised of JavaScript files and static HTML files using highly-customized jQuery code. 
### Documentation
There is no documentation for how to get the project running. All of the contextual information for how to run this project is lost and only exists in the codebase itself. The application is written using jQuery, which is shown throughout the codebase. But aside from that, there is no documentation that determines what code is running on what page. The only way to properly determine it is by troubleshooting the code and seeing in which file it fails. 
### Buildability
As a front-end project, this codebase isn’t buildable, but does run appropriately when the Alfresco Repo code is running. Since this is a JavaScript application, I will be judging buildability based on whether the JavaScript interactions in the code run without errors. Since there are no tests for this codebase, it is difficult to determine what parts of this codebase is functional or not.
### Interoperability
This codebase is tightly coupled with the previous codebases, Repo. The front-end code is an entirely custom jQuery project that attempts to be back-end agnostic even though it only supports this particular Alfresco Repository back-end and not any Alfresco Repository back-end. The project does not leverage the Alfresco Application Development Framework (ADF).
## Next Steps
- We’d like to hear your feedback about this preliminary evaluation. In particular, we’re interested in hearing about:
- What you learned from this document;
- If there are any areas that you’d like us to explore more;
- How we can incorporate a cost/benefit analysis into our evaluation, so that we consider the expense and time involved in refactoring code versus starting fresh; and
- FNS’s commitment to continued use of the Alfresco framework



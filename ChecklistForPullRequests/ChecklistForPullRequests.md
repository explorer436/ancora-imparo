https://github.com/google/eng-practices

https://github.com/google/eng-practices/tree/master/review

---------------------------------

This is a checklist that could be helpful when submitting and dealing with pull requests:

 1. Update the Jira ticket with the description about the work that is being done on the task. If the scope or the direction of the task changes mid-way through the implementation process, make sure that the Jira ticket is updated. This will serve as good documentation and help avoid having to answer multiple people on multiple occasions. This will prevent having to explain each and every change to each and every person reviewing the pull request. For anyone looking to find out why a change was made, the Jira ticket will have all the answers.
 2. Pull from master/develop - whichever one is supposed to be used according to team norms.
 3. Run the linters and unit tests before starting to make any changes - to make sure that everything looks good before you start making changes locally. yarn lint and yarn test.
 4. In test cases, if there is a chance to use tables, use tables instead of writing individual test cases. e.g. it.each with jest. This is also possible with junit.
 5. Test API locally for end-to-end integration.
 6. Make changes and test everything again - unit tests, integration tests, linters, etc.
 7. Push your changes.
 8. Deploy your branch to develop to make sure it works as expected in an environment other than local computer.
 9. Do you need to run regression and performance tests before merging these changes into the develop/master branch?
 10. If there is a new service integration, is the documentation updated? Update the README file if necessary. Are the manifest files updated? Alphabetical order for the lists in the manifest files.
11. Is there common code that can be put in a library as opposed to including it in the application itself?
12. Wherever possible, if things need to be added to constructors, put them in constructors - I'd ask myself: Should I re-use the same DependentService instance for all requests from the CurrentClass? Or do I need a new one for each request?
13. Do not put process variables or write code for process variables in test classes. Instead, mock them.
14. Passing parameters to constructors is a good idea instead of passing parameters to individual functions. Especially, if the methods use state and if they are not pure.
15. Make sure each layer like controller layer, service layer, etc. is doing what it is expected to do. Pay attention to separation of concerns. Things like validation should not seep into the deeper layers of the application. They should be handled as early as possible. Preferably, in the controller layer or in the service layer.
16. Wherever necessary, redact the sensitive data like passwords, tokens from printing on the logs.
17. In javascript, verify the use of single quotes can be replaced by backticks.
18. Go through the javadocs, jsdocs or descriptions for each single method and test case and verify if they are describing the method or test case appropriately. When method signatures are modified, make sure that the corresponding documentation on each method, test, etc. are also updated.
19. For javascript tests, make sure that there is a class level description at the top.
20. Create pull request and send it out for review.

---------------------------------

How to handle reviewer comments: https://github.com/google/eng-practices/blob/master/review/developer/handling-comments.md

You have to learn to not get emotionally attached to the code that you write. You have to deal with it objectively. If not, the comments on the pull requests are going to hurt you. There is a simple way to avoid this. Create pull requests and look at it from a third person's perspective.

Think about the comments and things that are being proposed on the pull requests objectively. There is a pretty good chance that the suggestions sometimes make sense. If the proposals make sense, go ahead and make the change.

If the proposals do not make sense, do not leave wiggle room when responding to comments on pull requests. If we leave nice responses, some people who need a lot of attention will take advantage of the situation and they tend to write essays about code quality in the comments.  Carefully write an explanation about why you think that the suggestion does not make sense and be firm about it. Sometimes, taking the conversation offline will help. This will give a chance for the two parties to sort out the differences and move on. Ultimately, we cannot get stuck with one single pull request. We have to move on.

---------------------------------

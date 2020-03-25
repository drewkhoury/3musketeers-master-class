# 3musketeers-master-class

## Things people want to learn about

- Make
- Examples/patterns
- some basic makefile overview might be nice…
- makefile patterns in 3 musketeers (target vs _target)
- when it’s better to package a script in the image vs attaching it as a volume
- Should every target be runnable just as well locally as it would in Jenkins?
- How important is it to try to ensure it can run on any platform?  If they are using Make and Gradle, where should certain logic go?  In Gradle? in Make? depends on ????


# Links

https://medium.com/@drew.khoury/optimizing-for-dx-the-developer-experience-f37fe168642d


# walkthrough

Start here: https://3musketeers.io/ (Test, build, and deploy your apps from anywhere, the same way.)

Consistency: Run the same commands no matter where you are.
Control: Control languages, version tools.
Confidence: Test your code and pipelines locally before your CI/CD tool runs it.

![3m](https://3musketeers.io/assets/img/diagrams-overview.3badd24e.svg "3m")




# Misc (to clean up later)

When a make file becomes complex that includes could help https://3musketeers.io/docs/make.html#multiple-makefiles ( https://3musketeers.io/docs/make.html

https://3musketeers.io/docs/patterns.html#docker is the pattern you're seeing us follow in most of the pipeline so far "Make calls directly Docker instead of Compose.

Everything that is done with Compose can be done with Docker." 

however also note "Using Compose helps to keep the Makefile clean." 

- https://3musketeers.io/docs/patterns.html#task-management-tool shows an example of how to implement an "npm" command "cleanly".

Notice that the compose file does all the volume mounting, workdir (and would do all the env injection etc).

Aside from reviewing all the different types of patterns and tips on the 3m site, I think we should really focus-in on how we "deliver/package" our functionality for each step/container. eg If we're going to offer a sonarqube-scanner image which is capable of invoking a sonarqube scan of your source it needs to have very clear:

- good documentation around authentication and connectivity (bonus points if the checks for auth and connectivity are explicitly when running the container and give you real examples of how to get it right or what the actual problem is)
- container/script inputs (what vars do I need to supply?, what sensible defaults/assumptions are we setting?, if/when we invoke the container with missing/no vars does the container fail with clear and sensible errors telling us exactly what's wrong and which vars it expects? will it helpful enough to show me what vars/folders it was looking for and what was missing?) <<< this should be baked into code, NOT figure it out by asking someone
- outputs in a standard and well understood format if they need to be consumed by other steps
- well understood options and config that allow you to make config changes rather than having to change the container each time (rather than mess around with compose/docker or doing ANY changes in make the container should allow for sensible configuration options, ie you might want to change behavior from "long running" to "fire and forget" or you may want to override the default path, you may want to accept a common config file but overridde only one variable instead of having to maintain your own config file, 

^^^^ All that comes down to how well we architect our scripts that we dockerize ... and that comes back to user experience (that's a joint effort on writing good software and improving as we go with ever use case).



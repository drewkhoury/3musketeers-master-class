# 3musketeers-master-class

## Things you'll learn in this master class ...

- Make
- Examples/patterns
- some basic makefile overview
- makefile patterns in 3 musketeers (target vs _target)
- when it’s better to package a script in the image vs attaching it as a volume
- Should every target be runnable just as well locally as it would in <insert specific build server>?
- How important is it to try to ensure it can run on any platform? If they are using Make and Gradle, where should certain logic go?  In Gradle? in Make? depends on ????

## Let's get started

[3musketeers-intro.md](3musketeers-intro.md)

## Advanced

### Make is difficult to use, and hard to learn

`make` is a powerful tool that can do a lot of things. However, the intent is to yse `make` as a simple interfact between your build tool and your build steps.

As you should only be using the most basic features of `make` it shouldn't be difficult to implement. If you're having a lot of difficulties, consider if you're over complicating your task.

Consider some real-life simple make files (easy to read, maintain and run):

- https://github.com/drewkhoury/devyo/blob/master/makefile
- https://github.com/drewkhoury/buildkite/blob/master/Makefile

You could consider using [multiple makefiles](https://3musketeers.io/docs/make.html#multiple-makefiles) or consider [another language](https://3musketeers.io/docs/make.html#complex-targets) if you have complex logic that demands it.

### I really don't want to use docker compose - I'm not even deploying anything / I'm using k8s

Don't confuse using `docker-compose` during your build/test steps with deploying your application in production. With 3musketers we're looking at the patterns we use to inteface with our build tool (like building and testing your application in your pipeline).

People often use compose files (with 3musketeers) to avoid having long and messy make files.

### To Compose or Not to Compose

If your use of docker is simple for a particular task, feel free to skip the compose file.

https://3musketeers.io/docs/patterns.html#docker

Make calls directly Docker instead of Compose. Everything that is done with Compose can be done with Docker. Using Compose helps to keep the Makefile clean.

When you have a multi-line docker invocation, or 5 lines of docker commands in a single task, consider if compose could simplify things for you.

https://3musketeers.io/docs/patterns.html#task-management-tool shows an example of how to implement an "npm" command "cleanly".

Notice that the compose file does all the volume mounting, workdir (and would do all the env injection etc).

Consider an even more complex senerio that invovled multiple services, logs, naming of containers, starting and stopping containers, cleanup when done.

### Who's fault is it anyway?

3musketeers **will not** stop you from writing bad pipelines or bad code.

3musketeers **will not** write your build steps for you.

3musketeers **will not** replace your build process or your build tool.

3musketeers **will not** deploy your application for you.

3musketeers **will not** store metadata or artifacts during your build process.

For example, if your project, team or organization creates a docker container to provide some sort of functionality (e.g a sonar scanner image) this docker image should have it's own:

- documentation
- development lifecycle
- versioning / latest tags in git and in it's artifact store
- versions should be immutable - never override a version with new code
- if the container is run without the approriate environment variables, it should set sensible defaults where it can, and fail with explict error messages where it can't set a defaults
- requirements about connectitity should be well documented (and properly testing with proper errors when there's lack of connecivity)
- auth should be clearly documented and variablized
- if volume mounts are required and if files are outputted, this should be clearly articulated

Making changes:

- scripts/containers should allow you to override config files and/or supply additional config files or variables to override defaults (thus reducing the need to change the container/script itself each time)
- if your container is really a packaging mechinisum for a script consider how the script will be used and if it's better to be baked into the container (ie each change to the script should cause a new version of the container) or if you'd like users to maintain the script themselves and simply call the container with the script mounted into it



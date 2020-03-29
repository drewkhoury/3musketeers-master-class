# The "Why"

I know how to build my own projects. Why should we put so much effort into our pipelines?

https://medium.com/@drew.khoury/optimizing-for-dx-the-developer-experience-f37fe168642d

# 3 musketeers

https://3musketeers.io/ (Test, build, and deploy your apps from anywhere, the same way)

- **Consistency:** Run the same commands no matter where you are.
- **Control:** Control languages, version tools.
- **Confidence:** Test your code and pipelines locally before your CI/CD tool runs it.

![3m](https://3musketeers.io/assets/img/diagrams-overview.3badd24e.svg "3m")

How to invoke:

```
# echo 'Hello, World!' with the following command
$ make echo
```

# When to use 3 musketeers

It's important to understand the goals of `Consistancy, Control and Confidence` and the part each tool plays in the pattern.

## Can't I just skip this and use my tools directly?

The benfitis of using these tools together might not be obvious if you've only worked in a single project, or in a small team or if you haven't seen a project grow in complexity over time.

You might also be new to tools such as `make`, `compose` and `docker` and as such the idea of introducing them into your pipeline might seem unessasary. This might be especially true if your team is working with legacy applications and you don't have any container presense in your organization or team.

Only your organization and your team can decide if the goals of `Consistancy, Control and Confidence` are worth the investment in pipeline standarization.

These patterns and tools truely shine when:

- Developers start to seek "fast feedback" by "shifting left" - ie wanting to run some tests early (before they commit code)
- Working in larger teams
- With different underlying development machines - or with developers who install different versions of software (how much time did a new developer spend getting a working build env?)
- Across multiple teams in large oragnizations
- With CI/CD agents managed by other teams where changes to agents are not easy and you don't have permission/flexibility (did someone upgrade a build agent and break how java works for you? how would you know?)
- When having to share code between vendors
- The more complex the application gets, or as more changes are made to the application and it's build steps (having to refactor or share build steps either within your team or between teams) 
- Testing your pipeline code (how many times have you done 20 check-ins of code just to test one bit of functionaility "on the build server")

# The 3 tools

As the name implies 3 musketeers is made up of 3 tools: https://3musketeers.io/about/tools.html

## Docker

Docker is the **most important musketeer of the three**. 

Many tasks such as testing, building, running, and deploying can all be done inside a lightweight Docker container.

The **portability of Docker** ensures you can **execute the same tasks, the same way, on different environments** like MacOS, Linux, Windows, and CI/CD tools.

Example: Docker can be invoked directly from `make`, or can be invoked from a `docker-compose` command in `make`.

## Make

Make is a cross-platform build tool to test and build software and it is used as an **interface between the CI/CD server and the application code**.

A single Makefile per application defines and encapsulates all the steps for testing, building, and deploying that application.

Of course other tools like rake or ant can be used to achieve the same goal, but having Makefile pre-installed in many OS distributions makes it a convenient choice.

```
# Makefile
echo:
	docker-compose run --rm alpine echo 'Hello, World!'
```

## Compose

Docker Compose, or simply Compose, manages Docker containers in a very neat way.

It allows multiple Docker commands to be written as a single one, which **allows our Makefile to be a lot cleaner and easier to maintain**.

Testing also often involves **container dependencies**, such as a database, which is an area where Compose really shines. No need to create the database container and link it to your application code container manually — Compose takes care of this for you.


```
# docker-compose.yml
version: '3'
services:
  alpine:
    image: alpine
```

## Can't I choose my own mukseteers?

Who says `make`, `compose`, `docker` are the perfect combo?

The key to `Consistancy, Control and Confidence` is not **only** in the specific combination of `make`, `compose`, `docker` but instead in the agreement of your team and your organization to use a standard that's easy for everyone to follow.

Consider:

- Do most of your development teams have easy access to `make`, `compose`, `docker` - or can you agree/reach a state where this is possible?
- Do you want to replace `make` with something else? (zeus, python, shell) Sure thing, just agree as a team what would be more easily to install and maintain
- Do you want to start with `Make` and `Docker` and introduce `Compose` only when the complexity demands it?

Next: [3musketeers-patterns.md](3musketeers-patterns.md)





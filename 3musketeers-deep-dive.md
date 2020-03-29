# Make

Make 101's:

- https://odino.org/makefile-101/
- https://devhints.io/makefile
- https://gist.github.com/isaacs/62a2d1825d04437c6f08

**https://3musketeers.io/docs/make.html**

- target vs _target
- .PHONY
- Docker and Compose commands as variables
- Target dependencies
- Pipeline targets
- make and target all
- Target and Single Responsibility
- Idempotency
- Targets .env and envfile
- Project dependencies
- Calling multiple targets in a single command
- Prevent echoing the command
- Continue on error
- Clean Docker and files
- Managing containers in target
- Multiple Makefiles
- Complex targets
- Self-Documented Makefile


Having a clean `Makefile` is key. It helps to understand it quickly and is easier to maintain.

https://3musketeers.io/docs/make.html#target-vs-target

`targetname` only requires make,compose docker and is expected to be available on the host
`_targetname` requires more and might not be available on the host (it's executed in a container or on a host if it has the requirements)

https://3musketeers.io/docs/make.html#complex-targets

If your make file is getting complex, consider if all the logic should be in `make` or if you can simplify it or push it down the stack.

# Docker

**https://3musketeers.io/docs/docker.html**

# Compose

**https://3musketeers.io/docs/compose.html**

# Environment Variables

**https://3musketeers.io/docs/environment-variables.html**

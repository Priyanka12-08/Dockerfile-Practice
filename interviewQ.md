Q: Why copy dependencies first?
A: To leverage Docker layer caching and speed up builds.

Q: Why alpine images?
A: Smaller size, faster pull, fewer vulnerabilities.

Q: CMD vs RUN?
A: RUN builds the image, CMD runs the container.
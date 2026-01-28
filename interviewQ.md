Q: Why copy dependencies first?
A: To leverage Docker layer caching and speed up builds.

Q: Why alpine images?
A: Smaller size, faster pull, fewer vulnerabilities.

Q: CMD vs RUN?
A: RUN builds the image, CMD runs the container.


Q Node.js dockerfile for port 8080

FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 8080
CMD ["node", "server.js"]

| Mistake            | Result                 |
| ------------------ | ---------------------- |
| Wrong COPY path    | Build fails            |
| Missing `COPY . .` | Runtime crash          |
| Wrong port         | App not accessible     |
| CMD in shell form  | Signal handling issues |

1️⃣ Why is WORKDIR used?

Answer:

WORKDIR /app sets the working directory inside the container.
All subsequent commands (COPY, RUN, CMD) run relative to this folder.
It keeps your container organized and avoids cluttering the root /.

2️⃣ Why package*.json and not copying all files first?

Answer:

We copy only package.json and package-lock.json first so Docker can cache the npm install step.
If we copied all source code first, every code change would trigger a full npm install, which is slower.
This is called Docker layer caching, a best practice in real-world DevOps.

3️⃣ Difference between RUN npm install and CMD node server.js
Instruction	Purpose
RUN npm install	Runs during image build → installs dependencies into the image.
CMD ["node", "server.js"]	Runs when container starts → actually launches the app.

💡 Remember:

RUN = build-time

CMD = runtime

4️⃣ Does EXPOSE actually publish the port?

Answer:

EXPOSE 8080 does not automatically make the container accessible.
It only documents which port the container will use.
To actually access the app, you must use port mapping when running the container:

docker run -p 8080:8080 my-node-app

✅ Extra Interview Tip

If asked “Why these steps in this order?”, you can answer:

“We first set the working directory, then copy only dependency files to leverage caching, install dependencies, copy app code, expose the port for documentation, and finally specify the start command for runtime execution.”


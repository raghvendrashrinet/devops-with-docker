# Chapter 2: Advanced Docker Operations

## Advanced Utility Commands (Bulk Actions)
These commands use shell substitution `$(...)` to pass a list of IDs from one command to another.

| Task | Command |
| :--- | :--- |
| **Stop all containers** | `docker stop $(docker ps -aq)` |
| **Remove all containers** | `docker rm $(docker ps -aq)` |
| **Remove all images** | `docker rmi $(docker images -q)` |
| **Kill and Remove** | `docker kill <name> && docker rm <name>` |

> **Tip:** The `-q` flag stands for "quiet," which returns only the Container/Image IDs.

---

## Container Inspection & Interaction
Once a container is running in the background (`-d`), use these to see what is happening inside:

### 1. Execute Processes (`exec`)
Use this to run a new process (like a shell) inside a container that is already running.
* `docker exec -it <container_name> bash` — Open an interactive terminal inside.
* `docker exec <container_name> ls -la` — Run a single command and see the output.

### 2. Logging (`logs`)
* `docker logs <container_name>` — View the current logs.
* `docker logs -f <container_name>` — **Follow** the logs in real-time (useful for the "looper" exercise).

### 3. Process Monitoring (`ps aux`)
To see the processes running *inside* the container:
1. Enter the container: `docker exec -it <name> bash`
2. Run: `ps aux`
### 4. Container pause and resume
	1. docker pause <container_name>
	2. docker unpause <container_name>
---

## Exercise 1.3: Secret Message
**Goal:** Use `exec` to find a message in a running container.
1. Run the image: `docker run -d --name secret-messenger devopsdockeruh/simple-web-service:ubuntu`
2. Enter the container: `docker exec -it secret-messenger bash`
3. Follow the log: `tail -f ./text.log`

## Exercise 1.4: Missing Dependencies
**Goal:** Install `curl` inside a running Ubuntu container.
1. Start the container: `docker run -it ubuntu`
2. Update packages: `apt-get update`
3. Install curl: `apt-get install -y curl`

## Running Shell Scripts
This example demonstrates how to run a background process directly from your terminal using an image like Ubuntu.
```bash
docker run -d -it --name looper ubuntu sh -c 'while true; do date; sleep 1; done'
```
- -d: Runs in detached mode (background).
- -it: Keeps it interactive and provides a TTY.
- sh -c '...': Tells the container to execute the string as a shell script.


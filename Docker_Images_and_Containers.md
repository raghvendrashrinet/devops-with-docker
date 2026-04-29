## Docker Images and Containers Explained
Docker Image Layers
A Docker image is built in layers.

Each instruction in a Dockerfile (e.g., FROM, RUN, COPY) creates a new layer.

Layers are immutable and cached, which makes builds efficient.

graph TD A[Base Layer: OS libraries] --> B[Layer 1: Installed packages] B --> C[Layer 2: App dependencies] C --> D[Layer 3: Application code] D --> E[Final Docker Image]

Creating a Container from an Image
A container is a running instance of an image.

When you run docker run , Docker:

Loads the image layers.

Adds a thin writable layer on top.

Starts the process defined in the image (e.g., CMD or ENTRYPOINT).

graph TD A[Image Layers] --> B[Writable Container Layer] B --> C[Running Container]

Relationship Between Image and Container
The container depends on the image: it uses all the read-only layers from the image.

The writable layer is unique to each container.

If you delete the container, the image remains intact.

Multiple containers can be created from the same image, each with its own writable layer.

graph TD A[Image] --> B[Container 1: Writable Layer] A --> C[Container 2: Writable Layer] A --> D[Container 3: Writable Layer]

Analogy: ISO vs Docker Image
An ISO file is a snapshot of an operating system.

When installed, the OS runs independently of the ISO.

A Docker image is different: containers always rely on the image layers.

Containers are not fully independent; they are tied to the image structure.

graph TD A[ISO File] --> B[Installed OS: Independent] C[Docker Image] --> D[Container: Dependent on Image]

Key Takeaways
Image = Blueprint (immutable, layered).

Container = Running instance (image + writable layer).

Containers are always related to their image, unlike ISO-installed OS which becomes independent.

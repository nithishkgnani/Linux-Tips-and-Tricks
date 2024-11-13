# ROS on Docker in Windows with GUI Support

Instructions to setup ROS2 on Docker in Windows with GUI support. In this example, I have taken the ROS humble version as the base image and made a Dockerfile to build the image. The Dockerfile is available [here](/Files/Dockerfile).

## Setup

Setup in Windows 10 with WSL2 with Docker Desktop.  

* Install Docker Desktop
* Install WSL2
* Install VcXsrv, an X Server for Windows
* Launch the X Server and configure it to allow connections from your Docker containers.
* In VcXsrv, select options like "Disable Access Control" to allow all clients to connect to the X Server.

To run a Docker container on Windows with both GUI support and a folder attached from the host system, you can follow these steps:

### 1. Set Up X Server for GUI Support

For Docker containers to display GUI applications on Windows, you need an X Server. Common options is:  
**VcXsrv**: [Download VcXsrv](https://sourceforge.net/projects/vcxsrv/)

1. **Install and Start VcXsrv**.
2. **Configure Access Control**: Allow connections from Docker by disabling access control in VcXsrv or enabling "No Access Control" mode in Xming.
3. **Get Your IP Address**: Open a command prompt and run `ipconfig` to find your local IPv4 address (something like `x.x.x.x`).

### 2. Prepare the Docker Run Command

We’ll use the `-v` flag twice in the `docker run` command:

* Once to mount the host folder.
* Once to set up the display environment variable (`DISPLAY`) for GUI support.

### 3. Running the Docker Container with GUI and Folder Mount

Assuming you want to:

* Mount a folder from your host system (e.g., `C:\Users\YourName\my_folder`) to a folder inside the container (e.g., `/data`).
* Enable GUI support for a GUI application.

Here’s the command structure:

```bash
docker run -e DISPLAY=<Your_IP>:0 \
           -v C:/Users/YourName/ros2_ws:/data \
           -v /tmp/.X11-unix:/tmp/.X11-unix \
           -it <image_name> /bin/bash
```

### Explanation of Each Part

* `-e DISPLAY=<Your_IP>:0`: Sets the `DISPLAY` environment variable in the container to route graphical output to your Windows machine. Replace `<Your_IP>` with your local IP address from Step 1.
* `-v C:/Users/YourName/ros-gazebo-lab/ros2_ws:/ros2_ws`: Mounts the folder `C:\Users\YourName\ros-gazebo-lab\ros2_ws` on the host to `/ros2_ws` in the container.
* `-v /tmp/.X11-unix:/tmp/.X11-unix`: Allows Docker to use the X Server on your host to display the GUI application.
* `-it <image_name> /bin/bash`: Runs the container in interactive mode and opens a bash shell. Replace `<image_name>` with your Docker image’s name.

### 5. Additional Tips

* **Permissions**: Ensure Docker Desktop has access to the shared folder. In **Docker Desktop** > **Settings** > **Resources** > **File Sharing**, add the host folder if it’s not already shared.

## Building the Docker Image and Running the Container

To build the image:  

* Download the [Dockerfile](/Files/Dockerfile) to your local machine.
* Open a normal terminal navigate to the folder containing the Dockerfile.
* Run the following commands in a Windows terminal (PowerShell):  

```bash
docker build --tag ros2humble:gui .
```

* In a different terminal, run `ipconfig` to get your local IP address.
* Back in initial terminal, run the image (using the same command as above):

```bash
docker run -e DISPLAY=<Your_IP>:0 -v C:\Users\YourName\ros-gazebo-lab\ros2_ws:/ros2_ws -v /tmp/.X11-unix:/tmp/.X11-unix -it ros2humble:gui
```

* This should provide you with both GUI support and folder access within your Docker container on Windows.
* To add a new terminal to the container, you can run the following commands in a new terminal window.

```bash
# Get the container ID
docker ps
# Run a new terminal in the container
docker exec -it <container_id> /bin/bash
```

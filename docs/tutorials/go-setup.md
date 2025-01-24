# Setting up a dev container for Go

* Primary author: [Arden Feldt](https://github.com/Arden-Feldt)

* Reviewer: [Siddhant Saxena](https://github.com/sisaxena42)

# Go Tutorial with Dev Containers

## Prerequisites

To follow along with this tutorial you'll need the following three things set up:

1. [Docker](https://www.docker.com/)
2. [Visual Studio Code](https://code.visualstudio.com/)
3. The [Remote - Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) installed in VSCode

!!! warning
    These must all be installed and open prior to moving on to the next step.

## Step-by-Step Guide

### Step 1: Set Up a Blank Project Directory

1. Create a new blank directory:

   ```title="bash"
   mkdir go-setup-proj
   cd go-setup-proj
   ```

2. Initialize a new git repository:

   ```title="bash"
   git init
   ```

### Step 2: Create a Dev Container Configuration

1. Create a `.devcontainer` directory:

   ```title="bash"
   mkdir .devcontainer
   ```

2. Inside `.devcontainer`, create a `devcontainer.json` file with the following content:

   ```title="json"
   {
     "name": "Go Dev Container",
     "image": "mcr.microsoft.com/devcontainers/go:latest",
     "features": {
       "ghcr.io/devcontainers/features/go:1": {
         "version": "latest"
       }
     },
     "customizations": {
       "vscode": {
         "extensions": [
           "golang.go"
         ]
       }
     }
   }
   ```

3. The key components of the configuration are:
   - **`image`**: Specifies the base image (Microsoft's Go Dev Container).
   - **`features`**: Ensures Go is installed and up-to-date.
   - **`customizations.vscode.extensions`**: Installs the official Go plugin by the Go Team at Google.

!!! note
    I'm not sure how much of all that is necessary but google said it was good and it worked for me.

### Step 3: Open the Dev Container

1. Open the folder in VSCode.
2. Ctrl+Shift+P and select **"Remote-Containers: Reopen in Container"**.

### Step 4: Verify Go Installation

1. Check the installed Go version:

   ```title="bash"
   go version
   ```

   Example output:

   ```
   go version go1.23.4 linux/amd64
   ```


### Step 5: Create a New Go Project
1. Initialize a Go module:

   ```title="bash"
   go mod init hello-comp423
   ```
2. Create a new file named `main.go` with the following content:

   ```title="go"
   package main

   import "fmt"

   func main() {
       fmt.Println("Hello, COMP423!")
   }
   ```
3. Run the program directly:

   ```title="bash"
   go run main.go
   ```

   Output:

   ```
   Hello, COMP423!
   ```

!!! warning
    If your output does not match "Hello, COMP423!", you've done goofed.

### Step 6: Build it like Bob

1. Build the binary:
   This creates an executable file named `hello`.
   ```title="bash"
   go build -o hello main.go
   ```
2. Run the built binary directly:

   ```title="bash"
   ./hello
   ```

   Output:

   ```
   Hello COMP423
   ```
3. **Difference between `go run` and `go build`:**

   - `go run`: Compiles and runs the code in one step, but does not create a standalone executable.

   - `go build`: Compiles the code and generates a standalone executable, allowing the program to be run without `go` installed.

!!! note
    This might feel familiar if you remember the comp211. I however do not, but cool regardless ig.

### Step 7: Commit Your Work

1. Add files to the repository:

   ```title="bash"
   git add .
   ```
2. Commit the changes:

   ```title="bash"
   git commit -m "That was easy as a gogo-squeeze"
   ```
3. Push it and you're done!

!!! note
    Ensure Docker is running before attempting to reopen the project in a container.
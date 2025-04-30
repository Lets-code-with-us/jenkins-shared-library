# Jenkins Shared Library

This shared library provides reusable pipeline functions for Jenkins to streamline CI/CD workflows.

## Overview

Jenkins Shared Libraries allow you to define common pipeline functionality that can be used across multiple Jenkins pipelines. This library contains utility functions for Docker operations and Git checkout functionality.

## Installation

### 1. Configure the Shared Library in Jenkins

1. Go to **Manage Jenkins** > **System** > **Global Pipeline Libraries**
2. Click **Add**
3. Configure the library:
   - **Name**: `your-shared-library-name` (use this name in your Jenkinsfile)
   - **Default version**: Specify a default version (e.g., `main`)
   - **Retrieval method**: Select Git and provide your repository URL
   - **Load implicitly**: Optional, check if you want to load the library automatically

### 2. Repository Structure

Ensure your repository follows the standard Jenkins shared library structure:

```
(root)
+-- src                     # Groovy source files
|
+-- vars                    # Global variable scripts
|   +-- dockerComposeRestart.groovy
|   +-- gitCheckout.groovy
+-- resources               # Resource files (optional)
+-- README.md
```

## Available Functions

### dockerComposeRestart

Stops and restarts Docker Compose services.

```groovy
// In your Jenkinsfile
pipeline {
    agent any
    stages {
        stage('Restart Docker Compose') {
            steps {
                dockerComposeRestart()
            }
        }
    }
}
```

**Implementation (`vars/dockerComposeRestart.groovy`):**
```groovy
def call() {
    sh "docker compose down"
    sh "docker compose up -d"
}
```

### gitCheckout

Performs a git checkout from a specified GitHub URL and branch.

```groovy
// In your Jenkinsfile
pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                gitCheckout('https://github.com/your-org/your-repo.git', 'main')
            }
        }
    }
}
```

**Implementation (`vars/gitCheckout.groovy`):**
```groovy
def call(String githubURL, String branch) {
    git url: githubURL, branch: branch
}
```

## Usage in Jenkinsfile

### Basic Example

```groovy
@Library('your-shared-library-name') _

pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                gitCheckout('https://github.com/your-org/your-repo.git', 'main')
            }
        }
        
        stage('Build & Deploy') {
            steps {
                // Your build steps here
                
                // Restart Docker services
                dockerComposeRestart()
            }
        }
    }
}
```

### Advanced Example with Parameters

```groovy
@Library('your-shared-library-name') _

pipeline {
    agent any
    
    parameters {
        string(name: 'GIT_REPO', defaultValue: 'https://github.com/your-org/your-repo.git', description: 'Git repository URL')
        string(name: 'GIT_BRANCH', defaultValue: 'main', description: 'Git branch to build')
    }
    
    stages {
        stage('Checkout') {
            steps {
                gitCheckout(params.GIT_REPO, params.GIT_BRANCH)
            }
        }
        
        stage('Deploy') {
            steps {
                dockerComposeRestart()
            }
        }
    }
}
```

## Contributing

Please follow these guidelines when contributing to this shared library:

1. Create a new branch for each feature or bug fix
2. Write unit tests for new functionality
3. Ensure your code follows the Groovy style guidelines
4. Submit a pull request for review

## License

[MIT](https://choosealicense.com/licenses/mit/)

## Maintainers

- [@shu12388y](https://github.com/shu12388y/)
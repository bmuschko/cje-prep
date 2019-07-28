# Building Continuous Delivery (CD) Pipelines

## Writing and using a shared library

1. Set up a new GitHub repository named `jenkins-standard-go-pipeline`. It will define a standard pipeline definition for Go projects implemented as shared library.
2. Add the file `vars/standard.groovy` that defines the declarative pipeline as global variable. Make the Go tool name and golang-ci version configurable with the help of parameters.
3. Push the changes to the `master` branch and configure the shared library in Jenkins.
4. Configure the shared library for consumption in Jenkins with the name `go-pipeline`.
5. Set up a new GitHub repository named `go-project-by-template`. Initialize a new Go project by running `go mod init github.com/bmuschko/hello-world` and adding a simple `main.go` file.
6. Add a new `Jenkinsfile`. Consume the shared library and call the global variable.
7. Trigger a build and visualize the pipeline in Jenkins.

<details><summary>Show Solution</summary>
<p>

The directory structure of shared library repository should have the following structure.

```
.
└── vars
    └── standard.groovy

1 directory, 1 file
```

Define the pipeline as global variable in the file `standard.groovy`.

```groovy
def call(String goToolName = 'go-1.12', String golangCiVersion = 'v1.12.5') {
    pipeline {
        agent any
        tools {
            go "$goToolName"
        }
        environment {
            GO111MODULE = 'on'
        }
        stages {
            stage('Compile') {
                steps {
                    sh 'go build'
                }
            }
            stage('Test') {
                environment {
                    CODECOV_TOKEN = credentials('CODECOV_TOKEN')
                }
                steps {
                    sh 'go test ./... -coverprofile=coverage.txt'
                    sh "curl -s https://codecov.io/bash | bash -s -"
                }
            }
            stage('Code Analysis') {
                steps {
                    sh "curl -sfL https://install.goreleaser.com/github.com/golangci/golangci-lint.sh | bash -s -- -b $GOPATH/bin $golangCiVersion"
                    sh 'golangci-lint run'
                }
            }
            stage('Release') {
                when {
                    buildingTag()
                }
                environment {
                    GITHUB_TOKEN = credentials('GITHUB_TOKEN')
                }
                steps {
                    sh 'curl -sL https://git.io/goreleaser | bash'
                }
            }
        }
    }
}
```

Configure the shared library under _Manage Jenkins > Configure System_.

![Shared Library Configuration](./images/14-shared-library/shared-library-config.png)

The directory structure should look as shown below.

```
.
├── Jenkinsfile
├── go.mod
└── main.go

0 directories, 3 files
```

The `Jenkinsfile` uses the shared library and calls the global variable. Optionally, you can configure the pipeline by passing in parameters.

```groovy
@Library('go-pipeline') _

standard()
```

The resulting build will go through all the pipeline stages defined in the shared library.

![Pipeline View](./images/14-shared-library/pipeline-view.png)

</p>
</details>
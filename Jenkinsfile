pipeline {
  agent {
    kubernetes {
    cloud "sw-devops-cluster"
    namespace "devops"
    yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: jnlp
    image: jenkins/jnlp-slave:4.0.1-1-alpine
"""
    }
  }

  options {
    timestamps()
    buildDiscarder(logRotator(numToKeepStr: "10", artifactNumToKeepStr: "10"))
  }

  environment {
    NGCI_VERSION = "5.0"
  }

  parameters {
    string(name: "JSON_FILE", description: "JSON file path", defaultValue: ".ngci/ngci.json")
  }

  stages {
    stage("Init") {
      steps {
        script {
          library changelog: false, identifier: "ngci@$NGCI_VERSION"
          LoadNGCI()
        }
      }
    }
  }
}

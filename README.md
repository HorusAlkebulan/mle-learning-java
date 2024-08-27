# mle-learning-java
ML Engineering tools based on Java

## Setup

### Java

1. Ensure Java Extensions is installed and enabled in visual studio code.

2. Download and install OpenJDK using homebrew or binaries from <https://adoptium.net/download/>

```sh
brew update
brew install openjdk
```

NOTES:

```sh
For the system Java wrappers to find this JDK, symlink it with
  sudo ln -sfn /opt/homebrew/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk

openjdk is keg-only, which means it was not symlinked into /opt/homebrew,
because macOS provides similar software and installing this software in
parallel can cause all kinds of trouble.

If you need to have openjdk first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/openjdk/bin:$PATH"' >> ~/.zshrc

For compilers to find openjdk you may need to set:
  export CPPFLAGS="-I/opt/homebrew/opt/openjdk/include"
```

3. Install Maven using homebrew or download from <https://maven.apache.org/download.cgi>.

```sh
brew update
brew install maven
```

4. Create a launch.json and then a launch configuration using Java.

```json
    "version": "0.2.0",
    "configurations": [
        {
            "type": "java",
            "name": "Current File",
            "request": "launch",
            "mainClass": "${file}"
        },
        {
            "type": "java",
            "name": "Main",
            "request": "launch",
            "mainClass": "com.example.horusalkebulan.Main",
            "projectName": "demo"
        }
    ]
}
```

## References

* <https://code.visualstudio.com/docs/java/java-webapp>
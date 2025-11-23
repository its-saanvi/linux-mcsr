# Java

- Open up a terminal and type in these commands:

```bash
sudo dnf install java-21-openjdk
```

- This will install and setup the Java JDK for you.
- Remember! JDK versions will be named in the same format. So JDK 11 would be named as **java-11-openjdk** and so on. So if you want to install other versions of the JDK you follow the same format. Its easy, isn't it? :D
- To run .jar files, such as ModCheck or Ninjabrain Bot, you can use the following terminal command, replacing `<path/to/jarfile.jar>` with the actual path to the .jar file:

```bash
java -jar <path/to/jarfile.jar>
```

## GraalVM

- GraalVM is a Java runtime which runs slower to start with, but greatly speeds up as time goes on. Using GraalVM is recommended for running Minecraft when using SeedQueue.
  - To download it, look [here](https://www.graalvm.org/downloads/). Make sure to select **Java 21** along with `Linux x64` for the platform.
  - After downloading it, extract it somewhere and select the `java` binary file in the `bin` folder by right clicking your instance in Prism Launcher > Edit > Settings > Java > Java installation > Browse.

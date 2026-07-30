# Java

- **Installation**
  - **Fedora 44 and onwards** OpenJDK builds are removed in favor of Adoptium Temurin OpenJDKs, please follow following instructions to install Temurin OpenJDKs. Run these commands one after another.
    
    1.  ```bash 
        sudo dnf install adoptium-temurin-java-repository
        ```
    2.  ```bash
        sudo fedora-third-party enable
        ```
    3.  Install appropriate version using  `sudo dnf install temurin-<version>-jdk` replace `<version>` with the required version.
    Example:
        ```bash
        sudo dnf install temurin-21-jdk
        ```
    4. Once Temurin JDK is installed change default Java version of your system using following command and select Temurin JDK by typing appropriate number from JDK list and enter.
        ```
        sudo alternatives --config java
        ```
    5. Once you have set correct JDK, you can verify by running in the terminal `java --version` should get similar ouput where it shows current JDK being used, it should be the Temurin one.
        ```bash
        openjdk 21.0.12 2026-07-21 LTS
        OpenJDK Runtime Environment Temurin-21.0.12+8 (build 21.0.12+8-LTS)
        OpenJDK 64-Bit Server VM Temurin-21.0.12+8 (build 21.0.12+8-LTS, mixed mode, sharing)
        ```
  - **Fedora 43 and below versions**
    - Open up a terminal and type in these commands:
      ```bash
      sudo dnf install java-21-openjdk
      ```
    - This will install and setup the Java JDK for you.
    - Remember! JDK versions will be named in the same format. So JDK 11 would be named as **java-11-openjdk** and so on. So if you want to install other versions of the JDK you follow the same format. Its easy, isn't it? :D

- **Running Jar files**

  To run .jar files, such as ModCheck or Ninjabrain Bot, you can use the following terminal command, replacing `<path/to/jarfile.jar>` with the actual path to the .jar file:

  ```bash
  java -jar <path/to/jarfile.jar>
  ```

## GraalVM

- GraalVM is a Java runtime which runs slower to start with, but greatly speeds up as time goes on. Using GraalVM is recommended for running Minecraft when using SeedQueue.
  - To download it, look [here](https://www.graalvm.org/downloads/). Make sure to select **Java 21** along with `Linux x64` for the platform.
  - After downloading it, extract it somewhere and select the `java` binary file in the `bin` folder by right clicking your instance in Prism Launcher > Edit > Settings > Java > Java installation > Browse.

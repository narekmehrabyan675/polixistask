# Documentation for the Program Using Apache Kafka

## Program Description

The program consists of three main components:

1. **Producer (LocationProducer)**

   - Generates random coordinates (latitude, longitude) with a specific step and sends them to the Kafka topic `location_updates`.

2. **Consumer (LocationConsumer)**

   - Reads messages from the `location_updates` topic.
   - Calculates the distance between consecutive locations using the Haversine formula.
   - Stores the total traveled distance and sends it to the Kafka topic `distance_report`.

3. **DistanceReport**

   - Subscribes to the `distance_report` topic and displays the total traveled distance in the console.

---

## Running the Program via IntelliJ IDEA

### Requirements

1. Installed **IntelliJ IDEA Ultimate/Community Edition**.
2. Loaded project with the correct package structure:
   - `producer.LocationProducer`
   - `consumer.LocationConsumer`
   - `report.DistanceReport`

### Step-by-Step Process

1. **Open the Project in IntelliJ IDEA**:

   - Ensure all dependencies (e.g., Apache Kafka, Gson) are installed and configured via Maven.

2. **Run servers Kafka and ZooKeeper
   - Open PowerShell and write
     - cd kafkaPath;
     - .\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties
   -Stay that windows opened.
   -Now open new window of PowerShell and write them
      -cd kafkaPath
      -.\bin\windows\kafka-server-start.bat .\config\server.properties

3. **Run the Producer**:

   - Navigate to the `LocationProducer` class.
   - Right-click on the `main()` method and select "Run 'LocationProducer.main()'".

4. **Run the Consumers**:

   - First, run `LocationConsumer`:
     - Navigate to the `LocationConsumer` class.
     - Right-click on the `main()` method and select "Run 'LocationConsumer.main()'".
   - Then, run `DistanceReport`:
     - Navigate to the `DistanceReport` class.
     - Right-click on the `main()` method and select "Run 'DistanceReport.main()'".

5. **Monitoring**:

   - In the IntelliJ IDEA console, you will see:
     - Locations sent by the Producer.
     - Distances calculated by the Consumer.
     - The total result displayed in `DistanceReport`.

---

## Running the Program via PowerShell

To automate the launch of all components, use a PowerShell script.
But on my PC shell scrypt dont work, didn't lounch kafka broker server, when it was in folder of project.If you have problem like that, please paste scrypt file the other space, that helps me and scrypt started to work.

### Setup Steps

1. **Created a PowerShell Script**
   Saved the following code in a file named `start_kafka_project.ps1`:


2. **Specify Paths**

   - Replace `C:\path\to\kafka` with the path to your Kafka installation.
   - Replace `target\location-tracking-app.jar` with the path to your JAR file(Project File).

3. **Run the Script**

   - Open PowerShell.
   - Navigate to the folder where `start_kafka_project.ps1` is saved.
   - Execute the script:
     ```powershell
     .\start_kafka_project.ps1
     ```

### What the Script Does:

1. Starts ZooKeeper and Kafka Broker.
2. Creates the topics `location_updates` and `distance_report`.
3. Launches Producer, LocationConsumer, and DistanceReport in separate terminal windows.

---

## Notes

- Ensure all topics are created before starting the Producer and Consumers.
- If running the program via PowerShell, ensure the execution policy is set correctly:
  ```powershell
  Set-ExecutionPolicy RemoteSigned
  ```
- For the program to work, Apache Kafka and ZooKeeper must be properly configured and running.



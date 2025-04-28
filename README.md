# ai-python-project-7--kafka-weather-data-solved
**TO GET THIS SOLUTION VISIT:** [AI-python Project 7- Kafka, Weather Data Solved](https://www.ankitcodinghub.com/product/python-p7-6-of-grade-kafka-weather-data-solved/)


---

📩 **If you need this solution or have special requests:** **Email:** ankitcoding@gmail.com  
📱 **WhatsApp:** +1 419 877 7882  
📄 **Get a quote instantly using this form:** [Ask Homework Questions](https://www.ankitcodinghub.com/services/ask-homework-questions/)

*We deliver fast, professional, and affordable academic help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;119430&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;2&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (2 votes)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;AI-python Project 7- Kafka, Weather Data Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (2 votes)    </div>
    </div>
Overview

For this project, imagine a scenario where you are receiving daily weather data for a given location. Your task is to populate this data into a Kafka stream using a producer Python program. A consumer Python program consumes data from the stream to produce JSON files with summary stats, for use on a web dashboard (you don’t need to build the dashboard yourself). Later in the project, you will also be visualizing some of the data collected by the consumer.

For simplicity, we use a single Kafka broker instead of using a cluster. A single producer will generate weather data (max temperature) in an infinite loop at an accelerated rate of 1 day per 0.1 seconds (you can change this during debugging). Finally, consumers will be different processes, launching from the same Python program.

Learning objectives: * write code for Kafka producers and consumers * apply streaming techniques to achive “exactly once” semantics * use manual and automatic assignment of Kafka topics and partitions

Before starting, please review the general project directions.

Clarifications/Correction

Nov 24: autograder.py added.

Nov 28: autograder bugfix: Added COPY statement to Dockerfile (required to run autograder correctly) Nov 30: autograder update: Increase timeouts and delays to ensure consistent test results

Container setup

Start by creating a files directory in your repository. Your Python programs and generated files must be stored in this directory. Next, build a p7 docker image with Kafka installed using the provided Dockerfile. Run the Kafka broker in the background using:

docker run -d -v ./files:/files –name=p7 p7

You’ll be creating three programs, producer.py, debug.py, and consumer.py. You can launch these in the same container as Kafka using: docker exec -it p7 python3 /files/&lt;path_of_program&gt;. This will run the program in the foreground, making it easier to debug.

All the programs you write for this projects will run forever, or until manually killed.

Part 1: Kafka Producer

Topic Initialization

Create a files/producer.py that creates a temperatures topic with 4 partitions and 1 replica. If the topic already existed, it should first be deleted.

Feel free to use/adapt the following:

“`python from kafka import KafkaAdminClient from kafka.admin import NewTopic from kafka.errors import UnknownTopicOrPartitionError broker = ‘localhost:9092’ admin_client = KafkaAdminClient(bootstrap_servers=[broker])

TODO: Create topic ‘temperatures’ with 4 partitions and replication factor = 1

print(“Topics:”, admin_client.list_topics()) “`

Weather Generation

Using the provided weather.py file, you can infinitely generate daily weather data starting from 1990-01-01 for a specific location (loosely modelled around weather of Dane County). Copy weather.py to your files directory and try generating some data using the following code snippet. This will generate the weather at a rate of 1 day per 0.1 second:

“`python import weather

Runs infinitely because the weather never ends

Next, instead of printing the weather, create a KafkaProducer to send the reports to the temperatures topic.

For the Kafka message’s value, encode the message as a gRPC protobuf.

For this, you’ll need to create a protobuf file report.proto in files with a Report message having the following fields, and build it to get a ??? _pb2.py file (review P3 for how to do this if necessary):

Requirements

1. Use a setting so that the producer retries up to 10 times when send requests fail

2. Use a setting so that the producer’s send calls are not acknowledged until all in-sync replicas have received the data

4. Use a .SerializeToString() call to convert a protobuf object to bytes (not a string, despite the name)

Running in Background

When your producer is finished, consider running it in the background indefinitely:

docker exec -d p7 python3 /files/producer.py

Part 2: Kafka Debug Consumer

Create a files/debug.py program that initializes a KafkaConsumer. It could be in a consumer group named “debug”.

The consumer should subscribe to the “temperatures” topic; let the broker automatically assign the partitions.

The consumer should NOT seek to the beginning. The consumer should loop over messages forever, printing dictionaries corresponding to each message, like the following:

Use your debug.py to verify your producer is writing to the stream as expected.

Part 3: Kafka Stats Consumer

Now you’ll write a files/consumer.py that computes stats on the temperatures topic, outputing results to JSON files after each batch. Partition Files

consumer.py will use manual partition assignment. If it is launched as docker exec -it p7 python3 /files/consumer.py 0 2, it should assign partitions 0 and 2 of the temperatures topic. Try out different setups for the consumers e.g. two consumer processes with two partitions each. Make sure you don’t miss out any partition when running your consumers.

Overview: * there are 12 months but only 4 partitions, so naturally some partitions will correspond to data from multiple months * each partition will correspond to one JSON file named partition-N.json (where N is the partition number), so there will be 4 JSON files * we might launch fewer than 4 consumer.py processes, so each process should be capable of keeping multiple JSON files updated

When a consumer launches that is responsible for partition N, it should check whether partition-N.json exists. If it does not exist, your consumer should first initialize it to {“partition”: N, “offset”: 0}.

Your consumer should then load partition-N.json to a Python dictionary. To manage each partition in memory, you might want another dictionary where each key is a partition number and each value is a dictionary with data for that partition.

When the partition-N.json files are loaded, your consumer should seek on each partition to the offset specified in the file.

Offset Checkpointing

After processing the messages in a partition of a batch, your consumer should check the current offset on the partition, use that to update the “offset” field in the partition dictionary, and write the partition out to the appropriate partition-N.json file.

Atomic Writes

Remember that we’re producing the JSON files so somebody else (not you) can use them to build a web dashboard. We will also use the JSON files to continously plot graphs. What if the dashboard app reads the JSON file at the same time your consumer is updating the file? It’s possible the dashboard or plotting app could read an incomprehensible mix of old and new data.

To prevent such partial writes, the proper technique is to write a new version of the data to a different file. For example, say the original file is

F.txt — you might write the new version to F.txt.tmp. After the new data has been completely written, you can rename F.txt.tmp to F.txt. This atomically replaces the file contents. Anybody trying to read it will see all old data or all new data. Here is an example:

python path = ???? path2 = path + “.tmp” with open(path2, “w”) as f: # TODO: write the data os.rename(path2, path)

Be sure to write your JSON files atomically.

Note that this only provides atomicity when the system doesn’t crash. If the computer crashes and restarts, it’s possible some of the writes for the new file might only have been buffered in memory, not yet written to the storage device. Feel free to read about fsync if you’re curious about this scenario.

Statistics

In addition to recording partition and offset, each partition-N.json file should have a key for each month seen in that partition; the corresponding value should be a dictionary with years as keys. Each year will correspond to yet another dictionary with stats about that month/year combination.

“`json { “partition”: 2, “offset”: 4117,

count: the number of days for which data is available. sum: sum of temperatures seen so far (yes, this is an odd metric by itself)

avg: the sum/count. This is the only reason we record the sum – so we can recompute the average on a running basis without having to remember and loop over all temperatures each time the file is updated

Exactly-Once Semantics (Recap)

Unless the producer repeatedly fails to write a message, each message/measurement should be counted exactly once in the output stats. We have alreading been providing directions on how to achieve this, but we repeat the details here for review.

To avoid undercounting: * the producer must use an ackowledgement option so that send is not considered successful until all in-sync replicas have received the data * the producer must use an option to retry up to 10 times upon failure to receive such an ack

Part 4: Plotting Stats

Create a plot.py program that we can run like this:

docker exec -it p7 python3 /files/plot.py

Here is some starter code:

“`python import pandas as pd import matplotlib.pyplot as plt

37.26354516129032 })

fig, ax = plt.subplots() month_series.plot.bar(ax=ax) ax.set_ylabel(‘Avg. Max Temperature’) plt.tight_layout() plt.savefig(“/files/month.svg”) “`

Your job is to read data from the partition-N.json files instead of hardcoding the numbers.

Each bar indicates the average max-temperature for a month stored in the partition JSON; when we have data for the same month across multiple years, use the most recent year.

Note: The weather data generated by weather.py represents the max-temperature for each day. So the average stored in your JSON partition files represents the “average max-temperature”.

Requirements: * you can hardcode that the partition numbers are 0-3. Do not hardcode the names of the files which contain the data for the three months we need, instead find them by iterating over the partition files * your code must work even if some of the JSON files do not exist * the order of the months along the x-axis doesn’t matter

Submission

All your code and generated plot should be in a directory named files within your repository.

We should be able to run the following on your submission to build and run the required image:

“`

To build the image

docker build . -t p7

To run the kafka broker

docker run -d -v ./files:/files –name=p7 p7

To run the producer program

docker exec -it p7 python3 /files/producer.py

To run the debug program

docker exec -it p7 python3 /files/debug.py

To run the consumer program (for partition 0, 2)

docker exec -it p7 python3 /files/consumer.py 0 2

To generate files/month.svg

docker exec -it p7 python3 /files/plot.py “`

Verify that your submission repo has a structure with at least the following committed:

. â”œâ”€â”€ Dockerfile â””â”€â”€ files â”œâ”€â”€ producer.py â”œâ”€â”€ debug.py â”œâ”€â”€ consumer.py â”œâ”€â”€ plot.py â”œâ”€â”€ report.proto â”œâ”€â”€ report_pb2.py â”œâ”€â”€ month.svg â””â”€â”€ weather.py

Testing

To run the autograder, you’ll need to have kafka-python and grpcio-tools installed on your VM. To do so, run the following command: pip3 install kafka-python==2.0.2 grpcio-tools

Afterwards, you can run the autograder using: python python3 autograde.py

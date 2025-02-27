# Sinks

The Sink serves as the endpoint for processed data that has been outputted from the platform,
which is then sent to an external system or application. The purpose of the Sink is to deliver 
the processed data to its ultimate destination, such as a database, data warehouse, visualization 
tool, or alerting system. It's the opposite of the Source vettex, which receives input data into the platform.
Sink vertex may require transformation or formatting of data prior to sending it to the target system. Depending on the 
target system's needs, this transformation can be simple or complex.

A pipeline can have many Sink vertices, unlike the Source vertex.

Numaflow currently supports the following Sinks

* [Kafka](./kafka.md)
* [Log](./log.md)
* [Black Hole](./blackhole.md)
* [User Defined Sink](./user-defined-sinks.md)

A user-defined sink is a custom Sink that a user can write using Numaflow SDK when 
the user needs to output the processed data to a system or using a certain transformation that is not 
supported by the platform's built-in sinks.  As an example, once we have processed the input messages, 
we can use Elasticsearch as a User defined sink to store the processed data and enable search and 
analysis  on the data.


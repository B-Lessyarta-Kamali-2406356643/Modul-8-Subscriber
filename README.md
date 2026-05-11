# Understanding subscriber and message broker 
## a. What is amqp?
AMQP stands for Advanced Message Queuing Protocol. It is a protocol used for communication between applications through a message broker. In this tutorial, AMQP is used by the subscriber and publisher to communicate with RabbitMQ.
## b. What does it mean? guest:guest@localhost:5672 , what is the first guest, and what is the second guest, and what is localhost:5672 is for?
In the URL amqp://guest:guest@localhost:5672, the first guest is the username, the second guest is the password, and localhost:5672 is the address and port of the RabbitMQ message broker running on the local machine.
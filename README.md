# Understanding subscriber and message broker 
## a. What is amqp?
AMQP stands for Advanced Message Queuing Protocol. It is a protocol used for communication between applications through a message broker. In this tutorial, AMQP is used by the subscriber and publisher to communicate with RabbitMQ.
## b. What does it mean? guest:guest@localhost:5672 , what is the first guest, and what is the second guest, and what is localhost:5672 is for?
In the URL amqp://guest:guest@localhost:5672, the first guest is the username, the second guest is the password, and localhost:5672 is the address and port of the RabbitMQ message broker running on the local machine.
## Simulating Slow Subscriber
In this simulation, I uncommented `thread::sleep(ten_millis);` in the subscriber program. This makes the subscriber wait for 1 second before processing each message.
When I run the publisher several times quickly, the publisher sends messages faster than the subscriber can consume them. Because of that, the total number of queued messages can increase in RabbitMQ. In my screenshot, the queued messages briefly increased and then decreased again after the subscriber processed them.
![Slow Subscriber](images/slow-subscriber.png)
## Reflection and Running at Least Three Subscribers

When I run at least three subscribers at the same time, RabbitMQ distributes the messages among the active subscribers. This makes message processing faster compared to using only one subscriber, because the workload is shared by multiple consumers.

In my experiment, the RabbitMQ dashboard shows multiple active connections and consumers. This means that more than one subscriber is connected to the message broker and ready to consume messages from the queue.

This experiment shows that event-driven architecture can help handle slow processing. Instead of depending on a single subscriber to process all messages, we can run multiple subscribers so messages can be consumed in parallel.

One possible improvement in the code is to handle errors from `publish_event` and `listen` more explicitly instead of ignoring the result with `_ =`. Another improvement is to avoid using an empty infinite loop in the subscriber and replace it with a clearer shutdown mechanism.

![Three Subscribers Console](images/three-subscribers-console.png)

![Three Subscribers RabbitMQ](images/three-subscribers-rabbitmq.png)
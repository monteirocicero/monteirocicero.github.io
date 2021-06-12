---
layout: post
title:  "Communication with low latency and high throughput with gRPC"
date:   2021-06-12 18:14:43 -0300
categories: grpc api
---


# gRPC
Actually, we live in the era of the microservices and cloud natives, and then, our application needs to communicate with another application over the network. In some cases it is a critical process that needs to happen very fast, for this instead of using a REST API to connect between services, we could use a technology that gains more attention every time, gRCP.
Remote calls existed a long time ago, in the 1970 decade we had the calls between files on the networking, then in the era of the oriented object the CORBA is the technology to distributed communication, after that RMI with popularity on the Java platform until coming to gRPC.
The model of gRPC is the simple client and server, where we define the contract on the server side and the client implements it. The contract is agnostic over programming languages. We could generate the stubs or proxies(Proxy Design Pattern) to connect to the server. With it, it is possible to build a server in Java and a client in Golang, for example.

![grpc](/assets/grpc_client_server.png)
>source: https://grpc.io/docs/what-is-grpc/introduction/


The image below is what happens to the real system.

![grpc](/assets/grpc-implementation.png)
>source: https://docs.microsoft.com/pt-br/dotnet/architecture/cloud-native/grpc


The above image shows how it works.
We could have 3 models of communication on the gRPC:
Unary, in this model we have a simple call from client to server, that receives the request, processes it and responds to the client and ends the communication.
Streaming, this model we could have such a client as a server receiving data until the end of the streaming data. The gRPC guarantees the messages orders.
The last model is bidirectional streaming, the requests and responses could happen in parallel on arbitrary order.
To define the services or contract, gRPC uses an IDL(Interface Definition Language) called Protocol Buffer.


# HTTP/2
Grpc is the platform and http/2 is the transport. Because the http/2 gRPC is so fast too. Http/2 comes with a lot of improvements over HTTP 1.1. The image below shows us how long time was necessary to have a bigger update on the protocol.

![grpc](/assets/http-timeline.png)
>source: https://kinsta.com/pt/aprenda/http2/


# Multiplexing

Multiplexing is an interesting feature that comes with this update. In the traditional model of request/response on HTTP 1.1, we could make a single request per TCP connection between the server and client, however, now is possible to make multiple connections on the same TCP connection.
The time to get a connection is less than early. The cost of getting a connection is bigger because the client and server make a handshake to establish the communication, with that, the throughput increases.


![grpc](/assets/mutiplexing.png)
>source: https://developers.google.com/web/fundamentals/performance/http2


# Header Compression

Another feature that makes the communication performative, the http/2 remembers the HTTP header, when the same request occurs and just only fields change, on the second call this field is sent.

![grpc](/assets/header-compression.png)
>source: https://developers.google.com/web/fundamentals/performance/http2


# The protocol Buffers

Known as Protobuf too, it's a neutral language created by Google to specify the structure that will be serialized, like a JSON or XML, but protobuf makes this more faster and smaller. There are fonts that say the serialization is faster than JSON 8x. It is good, because we can save money on the infrastructure if our environment has a massive serialization. Because protobuf is a binary protocol, the performance is better than working on a text file like JSON.


# Definition of service
The services are defined by contract on a file called proto file. This file has the methods and the message that go to exchange the server and client.


![subscriptions](/assets/profile_definition.png)
>source: https://grpc.io/docs/what-is-grpc/introduction/


The image above is a very simple definition of a service. And, the process to build this is in the image below.

![subscriptions-type](/assets/grpc_workflow.png)
>source: https://devopedia.org/grpc


After making the definition the server and client could be in a set of technologies, so put the files generated into the project.


# Summary
Grpc is an alternative to the REST API and makes more sense when we have a critical process that happens in real-time and should be low latency and high throughput. However, the model is different from REST, making the remote calls to be local. So it could be more complex.
A nice thing is the API first model with this approach is encouraged. And on a company that has a lot of microservices the CPU time used to serialize and deserialize JSON could be significant, with grcp the cost of CPUs may be decreased.


# Bibliography

[https://docs.microsoft.com/pt-br/dotnet/architecture/cloud-native/grpc](https://docs.microsoft.com/pt-br/dotnet/architecture/cloud-native/grpc)

[https://blog.lsantos.dev/guia-grpc-1/](https://blog.lsantos.dev/guia-grpc-1/)

[https://developers.google.com/web/fundamentals/performance/http2](https://developers.google.com/web/fundamentals/performance/http2)

[https://developers.google.com/protocol-buffers](https://developers.google.com/protocol-buffers)

[https://devopedia.org/grpc](https://devopedia.org/grpc)

[https://grpc.io/docs/what-is-grpc/introduction/](https://grpc.io/docs/what-is-grpc/introduction/)

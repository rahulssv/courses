# Dockerfile

## Ubuntu-DataSocket-Docker

```java title="Container1App.java"
import java.net.*;

public class Container1App {
    public static void main(String[] args) throws Exception {
        DatagramSocket socket = new DatagramSocket();
        byte[] sendData = "Hello, Rahul here!".getBytes();
        InetAddress receiverAddress = InetAddress.getByName("container2");

        DatagramPacket sendPacket = new DatagramPacket(sendData, sendData.length, receiverAddress, 9876);
        socket.send(sendPacket);
        socket.close();
    }
}
```

```java title="Container2App.java"
import java.net.*;

public class Container2App {
    public static void main(String[] args) throws Exception {
        DatagramSocket socket = new DatagramSocket(9876);
        byte[] receiveData = new byte[1024];

        DatagramPacket receivePacket = new DatagramPacket(receiveData, receiveData.length);
        socket.receive(receivePacket);
        String receivedMessage = new String(receivePacket.getData(), 0, receivePacket.getLength());

        System.out.println("Message received from Container 1: " + receivedMessage);
        socket.close();
    }
}
```
```python title="Dockerfile1"
# Dockerfile for Container 1
FROM ubuntu:latest

RUN apt-get update && \
    apt-get install -y openjdk-11-jdk

WORKDIR /usr/src/app
COPY Container1App.java .

RUN javac Container1App.java

CMD ["java", "Container1App"]
```

```python title="Dockerfile2"
# Dockerfile for Container 2
FROM ubuntu:latest

RUN apt-get update && \
    apt-get install -y openjdk-11-jdk

WORKDIR /usr/src/app
COPY Container2App.java .

RUN javac Container2App.java

CMD ["java", "Container2App"]
```

```bash title="runReceiver.sh"
docker build -t container1-image -f Dockerfile1 . ;
docker build -t container2-image -f Dockerfile2 . ;

docker network create "mynetwork" ;

docker run --name container2 --network mynetwork -it container2-image ;
```

```bash title="runSender.sh"
docker run --name container1 --network mynetwork -it container1-image ;
```

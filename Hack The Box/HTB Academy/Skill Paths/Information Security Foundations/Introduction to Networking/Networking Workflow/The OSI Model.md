- The **ISO/OSI** standard was created to ensure communication compatibility between different technical systems and devices.
- The **OSI model** consists of **seven layers**, each performing specific tasks to establish a connection.
- Layers **2-4** are **transport-oriented**, while layers **5-7** are **application-oriented**.
- Each layer provides services to the layer above it and relies on the layer below it for its tasks.
- Communication between two systems runs through all seven layers twice—once for the sender and once for the receiver.
- The sender processes the layers from **7** down to **1**, and the receiver processes the packet from **1** up to **7** to ensure security, reliability, and performance.

| **Layer**        | **Function**                                                                                                                                                                                                                |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `7.Application`  | Among other things, this layer controls the input and output of data and provides the application functions.                                                                                                                |
| `6.Presentation` | The presentation layer's task is to transfer the system-dependent presentation of data into a form independent of the application.                                                                                          |
| `5.Session`      | The session layer controls the logical connection between two systems and prevents, for example, connection breakdowns or other problems.                                                                                   |
| `4.Transport`    | Layer 4 is used for end-to-end control of the transferred data. The Transport Layer can detect and avoid congestion situations and segment data streams.                                                                    |
| `3.Network`      | On the networking layer, connections are established in circuit-switched networks, and data packets are forwarded in packet-switched networks. Data is transmitted over the entire network from the sender to the receiver. |
| `2.Data Link`    | The central task of layer 2 is to enable reliable and error-free transmissions on the respective medium. For this purpose, the bitstreams from layer 1 are divided into blocks or frames.                                   |
| `1.Physical`     | The transmission techniques used are, for example, electrical signals, optical signals, or electromagnetic waves. Through layer 1, the transmission takes place on wired or wireless transmission lines.                    |

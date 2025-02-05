2025-01-31 11:26

Status: 

Tags: [[CORE CS]]


# Computer Networks
# Chapter 1 :
## 1.1 What is computer networks?
A computer network is telecommunication network which allows digital devices(nodes) to exchange data between each other using wired or wireless connections to share resources (h/w or s/w), e.g. by internet

## 1.2 Goal of Computer Network 
1. Enable communication
2. Resource sharing
3. Data storage and access
4. cost efficiency by sharing resources
5. Reliability and redundancy, by alternate paths in case systems fails

## 1.3 Data Communication 
It is exchange of data between two devices via transmission medium. 
Components :
1. Message
2. Sender
3. Receiver
4. Transmission medium - Physical medium
5. Protocol - A set of rules for communication

## 1.4 Transmission mode
Data flow between two systems can be divided into 2 types
1. Simplex mode : One party is permanent sender and other party is permanent receiver. e.g. radio, mouse
2. Half-Duplex : Each station can transmit and receive, but not at the same time. When one send other receives and vice versa.
	- in Half duplex the entire capacity of channel is taken over by whichever of two devices is transmitting at the time.
	- e.g. Walkie-Talkie 
3. Full-Duplex : Both station can transmit and receive at the same time. Actually it's two half duplex connections.
	- The capacity of channel must be divided between two directions.
	- e.g. Telephone network

## 1.5 Network Criteria
A network must follow some criteria, some of the imp. are
1. Delivery and Accuracy 
2. Performance
3. Reliability
4. Security

## 1.6 Types of connections
1. Point to point connection : provides dedicated link between two devices. It is easier to manage these connections to a network admin
2. Multi-point : Here more than two specific devices share the single link

## 1.7 Physical topology
It refers to the way in which a network is laid out physically. It is a geometric representation of the relationship of all the links and linking devices to one another.
![[Network-Topology-Projects.png]]

1. Mesh topology : Every device has dedicated p-to-p link to every other device. We need $$ n*(n-1)/2 $$duplex mode links where n is number of nodes.   
	- Advantages : 
		1. No traffic problems.
		2. Robust
		3. Privacy and security
		4. Fault identification and fault isolation
	- Disadvantages :
		1. Installation and re-connections are difficult.
		2. The sheer bulk of wiring
		3. Expensive
2. Star topology : Each device has a dedicated p-to-p link only to central controller, usually called a hub. The device are not directly linked to one another.
	The controller acts as an exchange. If one device wants to send data to another, it will send to controller which then send data to the other device.
   - Advantage :
	   1. Less expensive than mesh.
	   2. Robust, but if hub fails everything fails.
	   3. Easy fault identification.
	- Disadvantages : 
		1. Dependency of the whole topology on one single point, the hub.
		2. Often more cabling is required in star than in some other topologies.
3. Bus topology : One long cable acts as backbone of the link, to all  the devices in the network.
	Nodes are connected to the bus cable by **drop lines and taps**.
	A drop line is connection running between the device and main cable.
	A tap is a connector, that either splices into the main cable or punctures the sheathing of a cable to create contact with metallic core.
	- Advantages :
		1. Easy installation.
		2. Use less cabling than mesh or star topology.
	- Disadvantages :
		1. Difficult re-connection and fault isolation.
		2. Difficult to add new devices to network.
		3. A fault or break in the bus cable stops all transmissions.
4. Ring topology : Each device has a dedicated p-to-p connection with only the two devices on either side of it.
	A signal is passed along the ring in one direction, from device to device. until it reaches the final destination. Each device in middle acts as a repeater. 
	- Advantages : 
		1. A ring is relatively easy to install and config.
		2. Fault isolation is simplified.
	- Disadvantages :
		1. A break in the ring (such as disabled station) can disable entire network.
		2. Very less secure, as data goes through intermediate station.

In actual everyone has it's own advantages and disadvantages, we choose as per our requirement, sometimes, hybrid too.


## 1.8 Types of network based on location
1. LAN :
	- local area network is limited to few kilometres of area. 
	- It may be privately owned and could be network inside an office on one of the floor or can be network connecting all PC of a building.
2. MAN : 
	- Metropolitan area network, is of size between LAN & WAN.
	- Its larger than LAN but smaller than WAN.
	- e.g. entire network of city.
3. WAN :
	- Wide area network is made up of all networks in large area.
	- The network in the entire state or country.

## 1.9 Network model
Every device is different over the network, thus we need a standard way to communicate between them.
International standard organisation (ISO) proposed **open system interconnection (OSI)** model that allows two systems to communicate regardless of their architecture differences.
 
## 1.10 OSI model
The purpose of OSI model is to tell how to communicate between different systems, without requiring changes to the logic of underlying hardware and software.
- The OSI model is **not a protocol**.
- It is model for understanding and designing a network architecture that is **flexible, robust and interoperable**. It consist of seven separate but related layers, each of which defines a part of the process of moving information across a network.
![[OSI model-1.png]]

![[OSCI model-2.png]]

- Layered architecture :
	- The OSI model is consist of 7 layers withing single machine. each layer calls upon the service of the later just below it and provides services to the layer above it. 
	- Between machines layer x on one machine communicates with layer x on another machine. This communications is done with agreed protocols.
	- The process on each machine that communicate at given layer are called peer-to-peer processes.
	- At physical layer communication is direct, data is sent in stream of bits.
	- At Higher layer, communication must move down through the layers on device A, over to device B, and then back up through the layers.
	- Each layer in sending devices adds it's own information to the message it receives from layer just above it, and passes whole package to below layer.
	- At receiving end message is unwrapped layer by layer, with each process receiving and removing the data meant for it.

1. **Physical layer:**
	- The physical layer defines the characteristics of the interface between the devices and the transmission medium. 
	![[OSI Layers_physical layer.jpeg]]
	- representation of bits: The physical layer data consist of stream of bits with no interpretation. To be transmitted, bits must be encoded into signals - electrical or optical. (analog--> digital -> digital)
	- Data rate: The data rate is number of bits sent each second. It is also defined by physical layer. 
	- Synchronization of bits : Both should send and receive same bits at same speed.
	- Line configuration: The physical layer is connected with the connection of devices to the media.
	- Physical topology: The physical topology is defines how devices are connected to each other to make network, and it is handled by this layer.
	- Transmission mode: The physical layer also defines the direction of the transmission between two devices, simplex, half-duplex or full-duplex.
2. **Data Link layer:** 
	- Framing: The data link layer divides the stream of bits received from the network layer into manageable data units called frames and also attaches header and trailer.
	![[OSI Layers_Data Link layer.jpeg]]
	- Physical addressing: If frames are to be distributed to different systems on the network, the data link layer adds a header to the frame to define the senders and/or receiver of the frame.
		e.g. Ethernet
	- Access Control: When two or more devices are connected to the same link, data link layer protocols are necessary to determine which device has control over the link at any given time.
	  **Multiple access protocols** are used for this. 
	  e.g. ALOHA, CSMA, Polling, etc.
	- Flow control: If the rate at which the data are absorbed by the receiver is less than rate at which data is produced in the sender, the data link layer impose a flow control mechanism to avoid overwhelming the receiver. used protocols can be **Sliding window**, etc.
	- Error handling: The data link layer adds reliability to the physical layer by adding mechanism to detect and re-transmit damaged or lost frames. It also uses mechanism to recognize duplicate frames. Error control is normally achieved by a trailer added to end of the frames.
		1. Error detection:
			- Two dimensional parity
			- Internet checksum
			- Cyclic redundant check(CRC)
		2. Error correction:
			- Hamming code
3. **Network Layer:**
	The network layer is responsible for the source-to-destination delivery of a packet, possibly across multiple networks(links).
	Full-fills source to destination delivery. The packet of data is called datagram in this layer. 
	![[source-to-destination-delivery-network-layer.png]]
	- Logical addressing: If packet passes the network boundary, we need another addressing system to help distinguish the source and destination systems. The network later adds a header to the packet coming from upper layer that, among other things include the logical addresses of the sender and receiver.
	  ![[logical-addressing.png]]
	- Routing: when independent networks or links are connected to create internet-works(network of networks) or a large network, the connecting devices(called routers or swiches) route or switch the packets to their final destination. One of the functions of the network layer is provide this mechanism. 
		- Routing protocols:
			- Intradomain - 
				1. Distance vector(RIP)
				2. Link state(OSPF)
			- Interdomain -
				1. Path vector(BGP)
4. **Transport layer**:
	- Service-point addressing: The transport layer header must include a type of address called a service-point address(or port address). The  network layer gets each packet to the correct computer; the transport layer gets the entire message to the correct process on the computer. The transport layer is responsible for process-to-process delivery of the entire message (port addressing and socket addressing). The packet of data is called segment in transport layer.
	- If we have to say, it's like transport layer does all the same work as data link layer does at local level....
	![[transport-layer-ports.png]]
	- Segmentation and reassembly: A message is divided into transmittable segments, with each segment containing a sequence number. These numbers enable the transport layer to reassemble the message correctly upon arriving at the destination and identify and replace packets which were lost in transmission. 
	- Congestion control: The transport layer can be either connections less or connection oriented. A connection-less transport layer treats each segment as an independent packet and delivers it to the transport layer of destination machine. A connection oriented transport layer makes a connection with receivers transport layer at fist before delivering packets. After all the data is transferred, the connection is terminated. 
	- Flow control: Like data link layer, the transport layer is responsible for for control. However, flow control is performed end to end rather than across the single link.
	- Error control: Error control at this layer is performed for process-to-process rather than across a single link.  Error correction is achieved through re-transmission.
5. **Session layer**: 
	The session layer is the network dialog controller. It establishes, maintains, and synchronizes the interaction among communicating systems.
	- The session layer is responsible for dialog control and synchronization.
	- Dialog control: The session layer allows two systems to enter into a dialog. It allows the communication between two processes to take place in either half duplex (one way at a time) or full-duplex (two ways at a time) mode.
	- Synchronization: The session layer allows a process to add checkpoints, or synchronization points, to a stream of data.
6. **Presentation layer:** 
	- Translation: The processes (running programs) in two systems are usually exchanging information in the form of character strings, numbers, and so on. 
	   - The information must be changed to bit streams before being transmitted. Because different computers use different encoding systems, the presentation layer is responsible for interoperability between these different encoding methods. 
	   - The presentation layer at the sender changes the information from its sender-dependent format into a common format. The presentation layer at the receiving machine changes the common format into its receiver-dependent format.
	- Encryption: To carry sensitive information, a system must be able to ensure privacy. Encryption means that the sender transforms the original information to another form and sends the resulting message out over the network. Receiver uses decryption to transform again to original data. 
	- Compression: Data compression reduces the number of bits contained in the information. Data compression becomes particularly important in the transmission of multimedia such as text, audio, and video
7. **Application layer**:  
	The application layer enables the user, whether human or software, to access the network. It provides user interfaces and support for services such as electronic mail, remote file access and transfer, shared database management, and other types of distributed information services.
	- Services 
		1. Network virtual terminal: A network virtual terminal is a software version of a physical terminal, and it allows a user to log on to a remote host. To do so, the application creates a software emulation of a terminal at the remote host. The user's computer talks to the software terminal which, in turn, talks to the host, and vice versa. The remote host believes it is communicating with one of its own terminals and allows the user to log on. 
		2. File transfer, access, and management: This application allows a user to access files in a remote host (to make changes or read data), to retrieve files from a remote computer for use in the local computer, and to manage or control files in a remote computer locally. 
		3. Mail services: This application provides the basis for e-mail forwarding and storage. 
		4. Directory services: This application provides distributed database sources and access for global information about various objects and services.

## 1.11 Transmission media 
(Layer 0) can broadly be defined anything that can carry information from source to destination.
1. Wired/ Guided media:
	1. Twisted pair cable (Ethernet cable)
	2. Coaxial cable (TV wire)
	3. Fibre optic cable
2. Wireless/unguided media -> ground propagation(short), sky propagation(long range), line of sight propagation(one direction)
	1. radio waves
	2. microwaves
	3. infrared waves

## 1.12 Switching 
Switching is the technique by which nodes control or switch data to transmit it between specific points on a network.
![[switching-cn.png]]
1. Circuit Switching: In circuit switching network resources (bandwidth) is divided into pieces and bit delay is constant during a connection.
	The dedicated path/circuit established between sender and receiver provides a guaranteed data rate. Data can be transmitted without any delays once the circuit is established. Telephone system network is the one of example of Circuit switching.
	- TDM (Time division multiplexing) : Divides into frames
		Time-division multiplexing (TDM) is a method of transmitting and receiving independent signals over a common signal path by means of synchronized switches at each end of the transmission line.
		TDM is used for long-distance communication links and bears heavy data traffic loads from end user.
		Time division multiplexing (TDM) is also known as a digital circuit switched.
	- FDM (Frequency Division Multiplexing): Divides into multiple bands
		Frequency Division Multiplexing or FDM is used when multiple data signals are combined for simultaneous transmission via a shared communication medium.
		It is a technique by which the total bandwidth is divided into a series of non-overlapping frequency sub-bands, where each sub-band carry different signal. Practical use in radio spectrum & optical fiber to share multiple independent signals.
	
2. Packet Switching: 
	- Datagram network - If the message is going to pass through a packet-switched network, it needs to be divided into packets of fixed or variable size. The size of the packet is determined by the network and the governing protocol.
	- In packet switching, there is no resource allocation for a packet. This means that there is no reserved bandwidth on the links, and there is no scheduled processing time for each packet. Resources are allocated on demand. The allocation is done on a first come, first-served basis.
	- When a switch receives a packet, no matter what is the source or destination, the packet must wait if there are other packets being processed. As with other systems in our daily life, this lack of reservation may create delay.
	- Even if a packet is part of a multipacket transmission, the network treats it as though it existed alone. Packets in this approach are referred to as datagrams. Packets may also be lost or dropped because of a lack of resources.
	- In most protocols, it is the responsibility of an upper-layer protocol to reorder the datagrams or ask for lost datagrams before passing them on to the application.
3. Virtual network: A virtual-circuit network is a cross between a circuit-switched network and a datagram network. It has some characteristics of both. Used nowadays in telephone networks.
	- Basically it fixes the path for the packets to travel, over the networks rather than going to destination from anywhere.

## 1.13 ISDN (Integrated Services Digital Network)
1. Definition: Integrated Services Digital Network - a set of protocols for establishing and breaking circuitswitched connections, and for advanced call features for the user. 
2. Development Period: Developed during the late 1980s and early 1990s. 
3. Digital Transmission: Unlike traditional telephone services which use analog signals, ISDN uses digital signals for transmission. 
4. Channels: ISDN provides channels known as B-channels (for data) and D-channels (for control and signaling).
5. BRI and PRI: There are two types of ISDN interfaces - Basic Rate Interface (BRI) and Primary Rate Interface (PRI). BRI is suitable for home and small enterprise, while PRI is used for larger installations. 
6. Speed: ISDN provides data rates up to 128 kbps in the case of BRI, and up to 1.544 Mbps for PRI in North America and 2.048 Mbps in Europe. 
7. Usage: Initially popular for internet access before the widespread availability of broadband. 
8. Decline: Its popularity has declined with the advent of faster, more reliable broadband internet services.
![[ISDN netowrk.png]]


# Chapter 2 : Data-link layer
- The data link layer is divided into two layers : **logical link control (LLC) (TOP) and media access control (MAC) (BOTTOM).** 
- Media Access Control (MAC): It defines the specific access method for each LAN, Ethernet and Take care of Addressing at the level (Lan technology).
- Flow control, error control, and part of the framing duties are collected into one sublayer called the logical link control (LLC).
- Framing is handled in both the LLC sublayer and the MAC sublayer.
## 2.1 Media Access control
When nodes or stations are connected and use a common link, we need a multiple-access protocol to coordinate access to the link. Many protocols have been devised to handle access to a shared link.
![[Media Access Control-CN.png]]
- Propagation Delay: Propagation delay is the time it takes for a bit to travel from point A to point B in the transmission media. 
  $TP = (Distance) / (Propagation  speed)$
- Transmission Delay(TT/TFR): A sender needs to put the bits in a packet on the line one by one. If the first bit of the packet is put on the line at time t1 and the last bit is put on the line at time t2 , transmission delay of the packet is $(t2 − t1 )$. 
  $Tt = (Packet length (L)) / (Transmission rate or Bandwidth (B)) = L / B$ 
1. **Random access protocols**: 
	- In random access methods, no station is superior to another station and none is assigned the control over another. No station permits, or does not permit, another station to send.
	- Two features give this method its name.
		- First, there is no scheduled time for a station to transmit. Transmission is random among the stations. That is why these methods are called random access.
		- Second, no rules specify which station should send next. Stations compete with one another to access the medium. That is why these methods are also called contention methods.
	- However, if more than one station tries to send, there is an access conflict-collision-and the frames will be either destroyed or modified.
	- All the protocols in Random access approach will answer the following questions
		- When can the station access the medium?
		- What can the station do if the medium is busy?
		- How can the station determine the success or failure of the transmission?
		- What can the station do if there is an access conflict?

	1. **ALOHA**: It was designed for a radio (wireless) LAN, but it can be used on any shared medium.
		- The idea is that each station sends a frame whenever it has a frame to send. However, there is the possibility of collision between frames from different stations.
		- We assume that the stations send fixed-length frames with each frame taking Tfr to send.
		- Vulnerable time in which there is a possibility of collision, we see that the time during which a collision may occur in pure ALOHA, is 2 times the frame transmission time. $Pure ALOHA vulnerable time= 2 x Tfr$
		![[ALOHA-CN.png]]
		![[aloha Protocols_Pure aloha strategy.jpeg]]
		- If all these stations try to resend their frames after the time-out, the frames will collide again.
		- Pure ALOHA dictates that when the time-out period passes, each station waits a random amount of time before resending its frame. The randomness will help avoid more collisions. We call this time the back-off time TB.
		- Pure ALOHA has a second method to prevent congesting the channel with retransmitted frames. After a maximum number of retransmissions attempts Kmax a station must give up and try later
	2. **Slotted ALOHA**: 
		- Pure ALOHA has a vulnerable time of 2 x Tfr. This is so because there is no rule that defines when the station can send. A station may send soon after another station has started or soon before another station has finished.
		- Slotted ALOHA was invented to improve the efficiency of pure ALOHA. In slotted ALOHA we divide the time into slots of Tfrs and force the station to send only at the beginning of the time slot.
		- Because a station is allowed to send only at the beginning of the synchronized time slot, if a station misses this moment, it must wait until the beginning of the next time slot. This means that the station which started at the beginning of this slot has already finished sending its frame.
		- Off course, there is still the possibility of collision if two stations try to send at the beginning of the same time slot (complete overlapping). However, the vulnerable time is now reduced to one-half, equal to Tfr.
		- If collision occurs then it is handled same like pure ALOHA, but difference is that it will be sent at start of slot, not anytime. 
		- It is more complex due to time synchronization for slots.
	3. **Carrier Sense Multiple Access(CSMA)**: 
		- To minimize the chance of collision and, therefore, increase the performance, the CSMA method was developed. The chance of collision can be reduced if a station senses the medium before trying to use it.
		- Carrier sense multiple access (CSMA) requires that each station first listen to the medium (or check the state of the medium) before sending, so "sense before transmit" or" listen before talk." CSMA can reduce the possibility of collision, but it cannot eliminate it.
		- The possibility of collision still exists because of propagation delay; when a station sends a frame, it still takes time (although very short) for the first bit to reach every station and for every station to sense it. In other words, a station may sense the medium and find it idle, only because the first bit sent by another station has not yet been received.
		- The vulnerable time for CSMA is the propagation time Tp. When a station sends a frame and any other station tries to send a frame during this time, a collision will result. But if the first bit of the frame reaches the end of the medium, every station will already have heard the bit and will refrain from sending. $$ Vulnerable time = propagation time $$
		- **Persistence Methods**: What should a station do if the channel is busy? What should a station do if the channel is idle?
		 Three methods have been devised to answer these questions:
			1. 1-persistent method: The 1-persistent method is simple and straightforward. In this method, after the station finds the line idle, it sends its frame immediately (with probability 1). This method has the highest chance of collision because two or more stations may find the line idle and send their frames immediately. (Basically station continuosly checks for line to empty, if it is then send immediately).
			2. Non-persistent method: In the non-persistent method, a station that has a frame to send senses the line. If the line is idle, it sends immediately. If the line is not idle, it waits a random amount of time and then senses the line again. This approach reduces the chance of collision because it is unlikely that two or more stations will wait the same amount of time and retry to send simultaneously. However, this method reduces the efficiency of the network because the medium remains idle when there may be stations with frames to send.
			3. P-persistent: The p-persistent approach combines the advantages of the other two strategies. It reduces the chance of collision and improves efficiency. In this method, after the station finds the line idle it follows these steps -->  1. With probability p, the station sends its frame. 2. With probability q = 1 - p, the station waits for the beginning of the next time slot and checks the line again, If the line is idle, it goes to step 1. If the line is busy, it acts as though a collision has occurred and uses the backoff procedure.
		1. **CSMA with Collision detection(CD)**: 
			- A station monitors the medium after it sends a frame to see if the transmission was successful. If so, the station is finished. If, however, there is a collision, the frame is sent again.
			- Minimum Frame Size - For CSMA / CD to work, we need a restriction on the minimum frame size. Before sending the last bit of the frame, the sending station must detect a collision, if any, and abort the transmission.
			- This is so because the station, once the entire frame is sent, does not monitor the line for collision detection. Therefore, the frame transmission time Tfr must be at least two times the maximum propagation time Tp.
			- To understand the reason, let us think about the worst-case scenario. If the two stations involved in a collision are the maximum distance apart, the signal from the first takes time Tp to reach the second, and the effect of the collision takes another time Tp to reach the first. So the requirement is that the first station must still be transmitting after 2Tp .
			![[CSMA-CD-CN.png]]
		2. **CSMA with collision avoidance(CA)**: 
			- In a wireless network, much of the sent energy is lost in transmission. The received signal has very little energy. Therefore, a collision may add only 5 to 10 percent additional energy. This is not useful for effective collision detection.
			- We need to avoid collisions on wireless networks because they cannot be detected. Carrier sense multiple access with collision avoidance (CSMA / CA) was invented for this network. Collisions are avoided through the use of CSMA / CA
			- three strategies: the interframe space, the contention window, and acknowledgment
			- Interframe Space (IFS) :
				- First, collisions are avoided by deferring transmission even if the channel is found idle. When an idle channel is found, the station does not send immediately. It waits for a period of time called the interframe space or IFS.
				- The IFS time allows the front of the transmitted signal by the distant station to reach this station. If after the IFS time the channel is still idle, the station can send, but it still needs to wait a time equal to the contention time. The IFS variable can also be used to prioritize stations or frame types.
			- Contention Window:
				- The contention window is an amount of time divided into slots. A station that is ready to send chooses a random number of slots as its wait time
				- The number of slots in the window changes according to the binary exponential back-off strategy
				- One interesting point about the contention window is that the station needs to sense the channel after each time slot.
				- However, if the station finds the channel busy, it does not restart the process; it just stops the timer and restarts it when the channel is sensed as idle. This gives priority to the station with the longest waiting time
			- Acknowledgment:
				- With all these precautions, there still may be a collision resulting in destroyed data. In addition, the data may be corrupted during the transmission. The positive acknowledgment and the time-out timer can help guarantee that the receiver has received the frame.
		![[CSMA-CA-CN.png]] ![[CSMA-CA-CN-2.jpeg]]
		
## 2.2 Flow Control
- To prevent data overflow, the receiving device has a buffer memory where incoming data are temporarily stored until processed; the data processing speed often lags behind the transmission rate.
- If the buffer is nearing its capacity, the receiver somehow must communicates with the sender to reduce the number of frames sent or pause transmission temporarily, ensuring smooth data flow and preventing system overload.
## 2.3 Error Control
(lost, out of order, corrupt) (detection and re-transmission)
- Error control, encompassing error detection and correction, enables the receiver to notify the sender about lost or damaged frames during transmission, facilitating the coordination for their re-transmission
- In the data link layer, error control is commonly implemented through the Automatic Repeat Request (ARQ) process, where detected errors trigger the retransmission of specific frames to maintain data integrity.

## 2.4 Sliding window protocol- Flow & Error control
1. **Stop-and-Wait Automatic repeat request(ARQ)**:
	- Receiver checks frames; corrupted ones are discarded silently(no ACK sent).
	- No ACK means sender re-transmits after timeout.
	- Sender keeps a copy of frame, starts a timer, and re-sends if no ACK is received.
	- Receiver does frame numbering, if frame comes out of order, it means lost/duplicate frames.
	- Sequence numbers: 
		- Frames are numbered using sequence numbers, added in a field within the data frame, to facilitate unambiguous communication with minimized frame size; the numbering can wrap around in a defined range. 
		- Sequence numbers only need to alternate between 0 and 1, enabling the receiver to differentiate between new frames and retransmitted frames without confusion, thereby optimizing the communication process.
	- Propagation Delay: Propagation delay is the time it takes for a bit to travel from point A to point B in the transmission media. TP = (Distance) / (Propagation speed)
	- Transmission Delay (TT): A sender needs to put the bits in a packet on the line one by one. If the first bit of the packet is put on the line at time t1 and the last bit is put on the line at time t2 , transmission delay of the packet is (t2 − t1 ). 
	  $Tt = (Packet length (L)) / (Transmission rate or Bandwidth (B)) = L / B$
	- Queuing Delay - It is measured as the time a packet waits in the input queue and output queue of a router. • Delayqu = The time a packet waits in input and output queues in a router.
	- Processing Delay - It is the time required for a destination host to receive a packet from its input port, remove the header, perform an error detection procedure, and deliver the packet to the output port or deliver the packet to the upper-layer protocol (in the case of the destination host).
	- $Total time = Tt (data) + Tp (data) + Dealyque + Delaypro + Tt (ack) + Tp (ack) + Dealyque + Delaypro$
	- Queuing delay and processing delays are generally kept 0. $Total Time = Tt (data) + Tp (data) + Tt (ack) + Tp (ack)$
	- In general we have taken Tt (ack) as negligible as the ack size is generally very less $Total Time = Tt (data) + Tp (data) + Tp (ack)$
	- $Total Time = Tt (data) + 2*Tp$  and $2*Tp$ is RTT.
![[stop-wait-arq-protocol-CN.png]]

2. **Go-Back-N ARQ**:
	- The Stop-and-Wait ARQ method can be inefficient for channels with high bandwidth, resulting in underutilization of the available data pipeline. Solution is Go-Back-N.
	- To enhance transmission efficiency, the Go-Back-N ARQ protocol allows multiple frames to be transmitted before acknowledgments are received, utilizing a "sliding window" concept.
	- The send window, an imaginary concept, covers the sequence numbers of frames that can be in transit, having a maximum size of $2^m - 1$. 
	- Sequence numbers are divided into four regions: the first represents acknowledged frames (no copies kept), the second represents frames sent but with unknown status (outstanding frames), the third denotes frames ready to be sent pending data packets from the network layer, and the fourth signifies sequence numbers inaccessible until the window slides further.
	- the receive window, with a constant size of one, ensures the receipt of correct data frames and the issuance of appropriate acknowledgments, discarding and necessitating the resending of any out-of-order frames.
	- Timer: Although there can be a timer for each frame that is sent, in our protocol we use only one. The reason is that the timer for the first outstanding frame always expires first; we send all outstanding frames when this timer expires.
	![[sliding-window-go-back-n-arq-CN.png]]
	![[go-back-n-cn.png]]
	- The receiver sends a positive acknowledgment for frames that arrive intact and in the correct order, whereas it remains silent and discards frames that are damaged or received out of sequence, maintaining a focus on the expected frame's arrival. 
	- The receiver's silence triggers the timer of the unacknowledged frame at the sender site to expire, prompting the sender to resend all frames from the one with the expired timer.
	- The receiver can issue a cumulative acknowledgment for multiple frames, enhancing efficiency.
	- To improve the efficiency of transmission (to fill the pipe), multiple packets must be in transition while the sender is waiting for acknowledgment.
	- In order to maximize the efficiency, the window size (Ws ) = (1+ 2a). Number of bits required for sequence numbers = ceil ( log2 (1 + 2a))
3. **Selective Repeat ARQ**:
	- Go-Back-N ARQ makes it easier for the receiver by only keeping track of one thing and ignoring frames that arrive in the wrong order. However, if the connection is not great, it can waste time and data by having to resend a bunch of frames often.
	- If the connection is not stable, the Selective Repeat ARQ is better as it only resends the frames that didn't arrive correctly, saving time and data. But, it makes the receiver's job a bit tougher.
	- The Selective Repeat ARQ also lets the receiver gather frames even if they come in the wrong order and keeps them until they can be arranged correctly and passed on, using equal room for storing and sending frames to work more efficiently.
	- In Selective Repeat ARQ, the data windows for sending and receiving are kept fairly small to manage data better $2^m-1$; each frame sent has its own countdown timer, making the tracking of requests quite similar to earlier methods but more detailed when data arrives.
	- When a clear NAK message arrives, we simply send the specific frame again; if a clear ACK message comes, we clear old data, stop the related countdown, and move the window's starting point. If a timeout happens, only the late frame is sent again.
	![[selective-repeate-arq-cn.png]]
4. **Piggybacking**: 
	- **Unidirectional protocols** mainly send data one way, but **ACK/NAK signals** go both ways.
	- **In practice, data flows bidirectionally**, requiring **piggybacking** to improve efficiency.
	- **Piggybacking** lets a data frame carry **control info** for the other direction.
	- Each node has **send & receive windows** and a **timer** managing request, arrival, and timeout.
	- This makes **arrival handling complex**, requiring a **uniform algorithm** at both sites.
## 2.5 Types of error
Data transmitted between nodes can sometimes be altered or corrupted during transmission. This corruption can manifest as either a single-bit error or a burst error.
a) A single-bit error refers to a scenario where only one bit in a data unit (like a byte or packet) is changed, either from 1 to 0 or vice versa. This type of error is less common.
b) Burst error, on the other hand, involves the alteration of two or more bits within a data unit. These changes might not be in successive bits. It's a more common error type as noise typically affects a set of bits, the extent of which is influenced by the data rate and noise duration.
1. **Hamming Distance:**
	- Hamming distance, represented as d(x, y), is a measure of the difference between two words of equal size, calculated by counting the number of dissimilar bits at the corresponding positions in the two words.
	- To find the Hamming distance, perform an XOR operation on the two words and count the number of 1s in the outcome.
	- For instance, the Hamming distance d(000, 011) equals 2, illustrated through the XOR operation: 000 XOR 011 equals 011, which has two 1s.
2. **Simple parity-check code:**
	- The simple parity-check code expands a k-bit dataword to an n-bit codeword (n = k + 1), with the additional bit serving as a parity bit to ensure an even total count of 1s in the codeword, though some variations aim for an odd/even count instead.
	- This code acts as a single-bit error-detecting mechanism, characterized by n = k + 1 and a minimum Hamming distance (dmin) of 2.
	- It is designed to identify an odd number of errors(for even parity check) within the data transmitted. ![[Simple Parity Check Code.jpeg]]
	- In the two-dimensional parity check, data words are arranged in a table with rows and columns. A special bit called a parity-check bit is added to each row and column to help identify errors in the data.
	- After the table is sent, the receiver checks the parity bits for each row and column to find "syndromes", which are indicators of where errors might have occurred.
	- This method can identify up to three errors in the table, but might miss errors if four or more bits are affected.
3. **Hamming codes:**
	- These are error-correcting codes originally designed to detect up to two errors or correct one single error.
	- The relationship between n and k in a Hamming code. The values of n and k are then calculated from r as $k = 2^r − r − 1$.
4. **Checksum**:
	- The checksum method is a way to check for errors when sending a list of numbers over the internet. In this method, we add up all the numbers we want to send and send this total sum, along with the original numbers.
	- At the receiving end, the numbers are added up again and compared with the received sum. If everything adds up correctly, it means that no errors occurred during transmission. Otherwise, it indicates that there was an error and the data is not accepted.For example, if the set of numbers is (7, 11, 12, 0, 6), we send (7, 11, 12, 0, 6, 36), where 36 is the sum of the original numbers. The receiver adds the five numbers and compares the result with the sum. 
	- We can make the job of the receiver easier if we send the negative (complement) of the sum, called the checksum. In this case, we send (7, 11, 12, 0, 6, -36). The receiver can add all the numbers received (including the checksum). If the result is 0, it assumes no error; otherwise, there is an error.
5. **Cyclic Codes**: Cyclic codes are special linear block codes with one extra property. In a cyclic code, if a codeword is cyclically shifted (rotated), the result is another codeword.
6. **Cyclic redundancy check**:
	- Sender **divides data by a fixed polynomial**, appends the remainder (CRC checksum).
	- Receiver **recomputes CRC**; if it matches, data is correct; else, error detected.
	- Efficient for **detecting burst errors** but **can’t correct errors**, only detect them.
	- **Widely used** in networks, storage devices, and communication protocols.![[CRC-CN.png]]
7. **Polynomials:** 
	- A pattern of 0s and 1s can be represented as a polynomial with coefficients of 0 and 1. The power of each term shows the position of the bit; the coefficient shows the value of the bit. An advantage is that a large binary pattern can be represented by short terms.
## 2.6 Ethernet
- Initially utilizing coaxial cables as a shared medium, modern Ethernet variations have adopted twisted pair and fiber optic links, coupled with hubs or switches, to facilitate communication and data transfer within LANs and MANs
- Over its evolution, Ethernet has boosted data transfer rates from an initial 2.94 Mbit/s to a remarkable 100 Gbit/s, offering several wirings and signaling options as part of the OSI physical layer in sync with Ethernet standards
- Data is divided into frames with addresses and error checks, enabling damaged frame detection and retransmission.
- Wi-Fi (IEEE 802.11) is a key wireless alternative to Ethernet in modern LANs.
- Uses a Bus topology, a shared communication line, optional acknowledgments, and Manchester encoding for data transmission.
- Standard Ethernet: Connectionless and Unreliable Service:
	- Each frame sent is independent of the previous or next frame. Ethernet has no connection establishment or connection termination phases. 
	- Ethernet is also unreliable, if a frame is corrupted during transmission and the receiver finds out about the corruption, the receiver drops the frame silently. 
	- In case of requirement ack can be sent separately at data packets.
![[Ethernet-CN.png]]
1. Preamble:
	- It is a 7-byte field that contains a pattern of alternating 0’s and 1’s. 
	- It alerts the stations that a frame is going to start. 
	- It also enables the sender and receiver to establish bit synchronization. 
	- The Preamble field is added at the physical layer.
2. Start Frame Delimiter (SFD):
	- It is a 1-byte field which is always set to 10101011. 
	- The last two bits “11” indicate the end of Start Frame Delimiter and marks the beginning of the frame. 
	- The SFD field is also added at the physical layer. 
	- Initial only SFD was there Preamble was added later
3. Destination Address:
	- It is a 6-byte field that contains the MAC address of the destination for which the data is destined. e.g. 2D : 8A : 7B : C5 
	- MAC address is present on NIC card. 
	- MAC address can be of three types 
		- Unicast-LSB of the first byte is 0 (Source address will always be unicast) 
		- Multicast- LSB of the first byte is 1, if we want to send, repeated messages to a group of station on the network then we can group these stations together and can assign a Multicast address to the group. 
		- Broadcast-all bit are assigned 1’s
4. Source Address: 
	- It is a 6-byte field that contains the MAC address of the source which is sending the data. 
	- Using some protocol, we can broadcast a request message asking MAC address of every other station in the network.
5. Length: 
	- As ethernet use variable size frames therefore we need Length field.
	- It is a 16-bit field.
6. Data: 
	- It is a variable length field which contains the actual data, also called as a payload field. 
	- The length of this field lies in the range [46 bytes, 1500 bytes], i.e. in an Ethernet frame, minimum data has to be 46 bytes and maximum data can be 1500 bytes. 
	- If it is less than 46 bytes, it needs to be padded with extra 0s. 
	- If more than 1500 bytes, it should be fragmented and encapsulated in more than one frame.
7. CRC: 
	- The last field contains error detection information. 
	- At the time of transmission CRC is calculated so it is in the last. 
	- It is a 4-Byte field

# Chapter 3 : Network Layer
- Source to Destination Delivery: Delivers packets from source to destination, possibly over multiple networks. 
- Logical Addressing: Uses logical addresses to identify the sender and receiver. 
- Routing: Responsible for finding the best route to send packets using routing protocols. 
- Packetizing: Involves encapsulating payload at the source, adding a header with essential details, and preserving payload integrity during transit, barring fragmentation cases. 
- Error and Flow Control: Encompasses adding a checksum in the datagram header for detecting corruption (not covering the entire datagram), with limited direct involvement in flow control, and using ICMP for some error control activities. 
- Congestion Control: Manages network congestion, handling situations when too many datagrams crowd a network segment and addressing capacity exceedance issues in networks or routers.
## 3.1 Internet protocol - IPv4 
 IPv4 operates as an unreliable connectionless datagram protocol, offering a best-effort delivery service which doesn't guarantee packet safety or order. 
-  The "best-effort" notion implies that IPv4 packets might experience corruption, loss, delays, or out-of-order arrival, potentially causing network congestion. 
- Employing a datagram approach, IPv4 treats each datagram independently, allowing them to traverse different routes to their destination. 	
- To enhance reliability, IPv4 should be coupled with a reliable protocol like TCP, forming the TCP/IP protocol stack for secured data delivery. ![[IPv4-header-CN.png]]
- Packets used by the IP are called datagrams. A datagram is a variable-length packet consisting of two parts: header and payload (data). The **header is 20 to 60 bytes in length** and contains information essential to routing and delivery.
	1. **Version Number**: The 4-bit version number (VER) field defines the version of the IPv4 protocol, which, has the value of 4. (Only hold value 0100 or 0110).
	2. **Header Length**: The 4-bit header length (HLEN) field defines the total length of the datagram header in 4-byte words. The IPv4 datagram has a variable-length header. 
	3. **Scaling factor**: To make the value of the header length (number of bytes) fit in a 4-bit header length, the total length of the header is calculated as 4-byte words. The total length is divided by 4 and the value is inserted in the field. The receiver needs to multiply the value of this field by 4 to find the total length. Example: If header length field contains decimal value 5 (represented as 0101), then Header length = 5 x 4 = 20 bytes.
	4. **Services Type**: IETF has changed the interpretation and name of this 8-bit field. This field, previously called service type, is now called differentiated services. Precedence is a 3-bit subfield ranging from 0 (000 in binary) to 7 (111 in binary). The precedence defines the priority of the datagram in issues such as congestion. If a router is congested and needs to discard some datagrams, those datagrams with lowest precedence are discarded first. ![[Service-type-ipv4-header-cn.png]]
	5. **TOS bits** is a 4-bit subfield with each bit having a special meaning. Although a bit can be either 0 or 1, one and only one of the bits can have the value of 1 in each datagram. ![[TOS-CN .png]]
	6.  **Total Length**: It defines the total length (header plus data) of the IP datagram in bytes. This field helps the receiving device to know when the packet has completely arrived. $Length of data = total length − (HLEN) × 4$
	7. **Identification**: 16-bit identification field identifies a datagram originating from the source host. To guarantee uniqueness, IP protocol uses a counter to label the datagrams. The counter is initialized to a positive number. When the IP protocol sends a datagram, it copies the current value of the counter to the identification field and increments the counter by one. When a datagram is fragmented, the value in the identification field is copied into all fragments, used for the identification of the fragments of an original IP datagram. The identification number helps the destination in reassembling the datagram. 
	8. **Fragmentation and fragmentation offset**: 
		1. Fragmentation is a process of dividing the datagram into fragments during its transmission. Datagram can be fragmented by the source host or any router in the path. The reassembly of the datagram, is done only by the destination host, because each fragment becomes an independent datagram. The fragmented datagram can travel through different routes. The bit numbers where the fragmentation is done is used as offset. 
		2. The 13-bit fragmentation offset field shows the relative position of this fragment with respect to the whole datagram. It is the offset of the data in the original datagram measured in units of 8 bytes. The bytes in the original datagram are numbered 0 to 3999. The first fragment carries bytes 0 to 1399. The offset value => 0/8 = 0. The second fragment carries bytes 1400 to 2799; the offset value => 1400/8 = 175. The third fragment carries bytes 2800 to 3999. The offset value => 2800/8 = 350.
	9. **Flag field**: 3 Bit flag defines three flags. The leftmost bit is reserved (not used). The second bit (D bit) is called the do not fragment bit. The third bit (M bit) is called the more fragment bit(it means the datagram is not the last fragment; there are more fragments after this one, if 0 means it's last fragment).
	10. **Time-to-Live(TTL**): 8 Bits. field in a datagram dictates the maximum number of hops (via routers) it can take, generally set to twice the highest number of routers between any two hosts. Every router the datagram passes through decreases the TTL value by one; the datagram is discarded if the TTL reaches zero, preventing it from circulating indefinitely due to potential routing table errors. Besides limiting a datagram's lifespan, the TTL field can be used to restrict a packet's journey deliberately, like confining it to a local network by setting the TTL value to 1, causing its discard at the first router.
	11. **Protocol**: In TCP/IP, the data section of a packet, called the payload, carries the whole packet from another protocol. A datagram, for example, can carry a packet belonging to any transport-layer protocol such as UDP or TCP. When the datagram arrives at the destination, the value of this field helps to define to which protocol the payload should be delivered.![[IPv4-header-protocolCN.png]]
	12. **Header Checksum**: The IP header checksum field only verifies the header, not the payload, indicating that IP is not entirely reliable as it doesn't affirm the payload remains unaltered during transmission. Due to alterations in fields such as TTL at every router, the checksum needs frequent recalculations. Upper-level protocols encapsulating data in the IPv4 datagram maintain separate checksums that cover the complete packet, thus the IPv4 datagram checksum doesn't validate the contained data. The IPv4 packet's header, which changes at each visited router (but not the data), is the only section included in the checksum, preventing unnecessary increases in processing time from recalculating the entire packet's checksum at every router
	13. **Source and Destination Address**: These 32-bit source and destination address fields define the IP address of the source and destination respectively.
	14. **Variable part**: The variable part comprises the options that can be a maximum of 40 bytes. Options, as the name implies, are not required for a datagram. They can be used for network testing and debugging.
		1. End of option: An end-of-option option is a 1-byte option used for padding at the end of the option field. It, however, can only be used as the last option.
		2. Record route: A record route option is used to record the Internet routers that handle the datagram. It can list up to nine router addresses. It can be used for debugging and management purposes.
		3. Strict Source Route: Strict Source Routing allows the sender to predetermine a specific path for a datagram, ensuring:
			1. Selection of a route with desired service (e.g., minimum delay, max throughput).
			2. Avoidance of insecure or competitor networks.
			3. The datagram must strictly follow the listed routers; deviation leads to discard and error.
			4. If any listed router is missed, the destination discards it with an error.
		4. Loose Source Route: A loose source route option is similar to the strict source route, but it is less rigid. Each router in the list must be visited, but the datagram can visit other routers as well.
		5. Timestamp: A timestamp option is used to record the time of datagram processing by a router. The time is expressed in milliseconds from midnight, Universal time or Greenwich mean time. Knowing the time, a datagram is processed can help users and managers track the behaviour of the routers in the Internet. We can estimate the time it takes for a datagram to go from one router to another. We say estimate because, although all routers may use Universal time, their local clocks may not be synchronized.
## 3.2 IPv6
Each packet is divided into two parts. Base header and Payload. The payload is made up of two parts : An optional extension header. The upper layer data. Base header has eight fields![[IPv6-Header-CN.png]]
1. **Version**: This is 4-bit field which defines the version number of IP. For IPv6, the value is 6.
2. **Priority**: The 4-bit priority field defines the priority of the packet with respect to traffic congestion.
3. **Flow label**: The flow label is a 3-byte field that is designed to provide special handling for a particular flow of data.
4. **Payload length**: The 2-byte payload length field defines the total length of IP datagram excluding the base header.
5. **Next header**: The next header is an 8-bit field defines the header that follows the base header in the datagram.
6. **Hop limit**: This 8-bit hop limit field serves the same purpose as TTL field in IPv4.
7.  **Source address**: The source address field is a 16-bytes internet address that identifies the original source of datagram.
8. **Destination address**: The destination address field is a 16-byte internet address that usually identifies the final destination of the datagram.
9. **Extension header**: Extension header field help in processing of data packets by appending different extension header. Each extension header has a length equal to multiple of 64-bits.
## 3.3 IPv4 vs IPv6
1. Address Length 
	1. IPv4: 32-bit (4 bytes) 
	2. IPv6: 128-bit (16 bytes) 
2. Address Notation 
	1. IPv4: Decimal (e.g., 192.168.1.1) 
	2. IPv6: Hexadecimal (e.g., 2001:0db8:85a3:0000) 		
3. Number of Addresses 
	1. IPv4: Approximately 4.3 billion 
	2. IPv6: Approximately 340 undecillion 
4. Configuration 
	1. IPv4: Manual or DHCP 
	2. IPv6: Stateless address autoconfiguration (SLAAC) or DHCPv6 
5. Security 
	1. IPv4: Initially lacked, added later as extensions 
	2. IPv6: Inbuilt support for IPsec, providing network security at the IP layer
## 3.4 Advancements in IPv6
- Larger Address Space: Can accommodate a virtually unlimited number of unique addresses, facilitating the growth of the internet. 
- Simplified Header: IPv6 has a simpler header structure, which improves the speed of routing by allowing routers to process packets more efficiently. 
- Improved Multicast: IPv6 utilizes multicast addressing to send data packets to multiple destinations in a single transmission, which conserves bandwidth compared to IPv4. 
- No NAT Required: IPv6 was designed to eliminate the need for NAT, making end-to-end connection more straightforward and reducing latency and complexity. 
- Mobility and Security: IPv6 was built considering modern requirements, offering better support for mobile devices and higher levels of security.

## 3.5 Need of Additional protocols 
- IP packets, however, need to be encapsulated in a frame, which needs physical addresses (node-to-node). We will see that a protocol called ARP, the Address Resolution Protocol. 
- We sometimes need reverse mapping-mapping a physical address to a logical address. For example, when booting a diskless network or leasing an IP address to a host, RARP is used. 
- Lack of flow and error control in the Internet Protocol has resulted in another protocol, ICMP, that provides alerts. It reports congestion and some types of errors in the network or destination host 
- IP was originally designed for unicast delivery, one source to one destination. As the Internet has evolved, the need for multicast delivery, one source to many destinations, has increased tremendously. IGMP gives IP a multicast capability.

## 3.5 Address Resolution Protocol(ARP)  
- The IP address of the next node alone is not helpful in moving a frame through a link; we need the link-layer address(MAC address) of the next node. 
- ARP maps an IP address to a logical-link address. ARP accepts an IP address from the IP protocol, maps the address to the corresponding link-layer address, and passes it to the datalink layer. 
- The ARP protocol is one of the auxiliary protocols defined in the network layer.
- Anytime a host or a router needs to find the link-layer address of another host or router in its network, it sends an ARP request packet. The packet includes the **link-layer and IP addresses of the sender and the IP address of the receiver.** 
- Because the sender does not know the linklayer address of the receiver, the query is broadcast over the link.
- Every host or router on the network receives and processes the ARP request packet, but only the intended recipient recognizes its IP address and sends back an ARP response packet.
- The response packet contains the recipient’s IP and link-layer addresses. The packet is unicast directly to the node that sent the request packet.
## 3.6 Reverse Address Resolution Protocol (RARP) 
- RARP finds the logical address for a machine that knows only its physical address. Each host or router is assigned one or more logical (IP) addresses, which are unique and independent of the physical (hardware) address of the machine. To create an IP datagram, a host or a router needs to know its own IP address.
- A RARP request is created and broadcast on the local network. Another machine on the local network that knows all the IP addresses will respond with a RARP reply.
- The requesting machine must be running a RARP client program; the responding machine must be running a RARP server program.

## 3.7 Internet Control Message Protocol(ICMP)
- The IP protocol has no error-reporting or error-correcting mechanism. The IP protocol also lacks a mechanism for host and management queries. A host sometimes needs to determine if a router or another host is alive. And sometimes a network administrator needs information from another host or router.
- The ICMP is designed to compensate these. It is companion to the IP protocol.
- ICMP messages are divided into two broad categories: Error-Reporting messages and query(request & reply) messages. The error-reporting messages report problems that a router or a host (destination) may encounter when it processes an IP packet. The query messages, which occur in pairs, help a host or a network manager get specific information from a router or another host.
1. **Error Reporting**: ICMP does not correct errors - it simply reports them. Error correction is left to the higher-level protocols. Error messages are always sent to the original source because the only information available in the datagram about the route is the source and destination IP addresses. ICMP uses the source IP address to send the error message to the source (originator) of the datagram. ![[Error-reporting-ICMP-CN.png]]
	- Time exceeded message : ICMP will take source IP from discarded packet and informs to the source, of discarded datagram due to time to live field reaches to zero, by sending time exceeded message.
	- Parameter problem: Whenever packets come to the router then calculated header checksum should be equal to received header checksum then only packet is accepted by the router. If there is mismatch packet will be dropped by the router. ICMP will take the source IP from the discarded packet and informs to source by sending parameter problem message.
	- Destination Un-reachable : Destination unreachable is generated by the host or its inbound gateway to inform the client that the destination is unreachable for some reason. There is no necessary condition that only router give the ICMP error message some time destination host send ICMP error message when any type of failure (link failure, hardware failure, port failure etc.) happen in the network.
	- Redirection message : Redirect requests data packets be sent on an alternate route. The message informs to a host to update its routing information (to send packets on an alternate route).
	- Note: 
		- No ICMP error message will be generated in response to data carrying an ICMP error message.
		- No ICMP error message will be generated for fragmented datagram that is not the first fragment.
		- No ICMP error message will be generated for a datagram having multicast address.
		- No ICMP error message will be generated for datagram having special address such as 127.0.0.0 or 0.0.0.0
2. **Query(request & reply)**: In addition to error reporting, ICMP can diagnose some network problems. This is accomplished through the query messages, a group of four different pairs of messages. 
	- In this type of ICMP message, a node sends a message that is answered in a specific format by the destination node. A query message is encapsulated in an IP packet, which in turn is encapsulated in a data link layer frame. ![[ICMP-Query-CN.png]]
	- Echo Request and Reply: Echo-request and echo-reply messages, encapsulated within IP datagrams, are essential diagnostic tools enabling network managers and users to pinpoint network issues and confirm that IP protocols in sender and receiver systems are in sync. Modern systems offer an advanced version of the ping command, capable of generating a series of these messages, facilitating comprehensive network analysis through the collection of vital statistical data.
	- Router Solicitation and Advertisement: A host sends a router-solicitation message to discover routers on its network. Routers respond with router-advertisement messages, providing routing information. Routers can also periodically send advertisements to announce their presence and other known routers.
	- Address-Mask Request and Reply: A host may know its IP address but not its subnet mask. It sends an address-mask-request to a router, either directly or via broadcast. The router replies with an address-mask-reply, providing the subnet mask.
	- Timestamp Request and Reply: Two machines (hosts or routers) can use the timestamp request and timestamp reply messages to determine the round-trip time needed for an IP datagram to travel between them. It can also be used to synchronize the clocks in two machines.

## 3.8 Internet Group Message Protocol(IGMP)
- The IP protocol can be involved in two types of communication: unicasting and multicasting. Unicasting is the communication between one sender and one receiver. It is a one-to-one communication. 
- However, some processes sometimes need to send the same message to a large number of receivers simultaneously. This is called multicasting, which is a one-to-many communication. 
- Multicasting has many applications. For example, multiple stockbrokers can simultaneously be informed of changes in a stock price, or travel agents can be informed of a plane cancellation.











# References

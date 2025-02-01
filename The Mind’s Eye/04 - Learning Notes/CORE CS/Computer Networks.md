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

## 2.4 Sliding window protocol-Flow & Error control
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
	- $Total Time = Tt (data) + 2*Tp$  and $2*Tp$ is RTT
















# References

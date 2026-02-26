# Jabber 
## Jabber Packet Protocol
___
Jabber is a application level packet protocol that uses encryption and onion routing to obscure the sender and recipiant of the packet. 

Jabber packets shall be encrypted using post-quantum encryption schemes at two layers, first a internal layer containing the content destined for the intended recipiant is created using the public key of the intended recipiant. Second on top of this layer, the packet is encrypted with the encryption key of the next hop address of the Jabber network. 

Each packet shall contain a unique hash that is used to identify the packet in the header, when a client receives a duplicate packet, there will be a 7% chance to not retransmit the packet. The idea of this probablistic system is to avoid having a TTL in the packet and to obscure exactly where the packet was first transmitted from. With a 7% chance to not retransmit on a duplicate packet, the packet will have a half life after the first loop of the circuit of 10 jumps. With this setup, for each of the 10 clients to transmit 1kB of data per second, each member of the loop must transmit a minimum of 30kB per second. From the perspective of the overall network, this is a effective usage of 33%, for a user, the 30kB is only 3% new user data being transmitted. 

Jabber Packets are intended to be sent in a unidirectional loop between ~10 clients. Each client shall have a unique upstream client that sends packets to the current client and to which the current client will send ACK messages to, and shall have a unique downstream client that the current client forwards packets to and receives ACK messages from on sucsesful delivery of the message.

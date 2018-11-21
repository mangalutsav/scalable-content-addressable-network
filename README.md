**Content Addressable Networks**
============================

Name : Utsav Mangal, Sandeep Pal, Akshat Bhardwaj, Abhishek Sharma, Aashutosh
Email : umangal@cs.iitr.ac.in, spal1@cs.iitr.ac.in, abhardwaj@cs.iitr.ac.in, asharma1@cs.iitr.ac.in, aashutosh@cs.iitr.ac.in

## **Instructions to compile**  

Run the following command
```
make
```

## **Bootstrap node**
Please go to src/com/can/nodes/Peer.java and update BOOTSTRAP\_HOSTNAME to correspond to the hostname of your bootstrap.

## **Start the bootstrap node**
```
java -cp content-addressable-network.jar com.can.nodes.Peer
```
*The Bootstrap node should now be up and running. Now go to any other machine on the network and run the above command*

## **Commands**

The following are the commands that are supported by this implementation of the content addressable network.  

### Build the network of machines

- Type JOIN and press enter on all the machines except the bootstrap node (it is already part of the network).
- The JOIN success message is displayed on all the nodes.
- Now all the nodes have joined the network and we can start performing operations.

### INSERT and SEARCH
- Inserting a keyword can be done from any peer. The following is the command for INSERT,  

  ```
  INSERT <keyword>
  ```  
  *The INSERT success message, along with information of the peer in which the keyword was inserted, is displayed. If the INSERT was not successful then a FAILURE message is displayed.*  

- We can now search for the keyword inserted from any of the peers. The following is the command for SEARCH,  

  ```
  SEARCH <keyword>
  ```
  *The SEARCH success message, along with the information of the peer from which the keyword was retrieved, is displayed. The route taken by the SEARCH request is also displayed. If the SEARCH failed (file not present) then a FAILURE message is displayed.*  

### LEAVE
- A node can decide to leave the network. Type the following command for the node to leave the network. A success message corresponding to the LEAVE operation is displayed.  

  ```
  LEAVE
  ```
  *The node can now rejoin the network by typing 'JOIN'.*

## **Sample test runs and corresponding outputs**

- Running the content addressable network on the following nodes,  

  * \<hostname of bootstrap node\> (bootstrap node)
  * \<hostname of server 1\>
  * \<hostname of server 2\>
  * \<hostname of server 3\>

- Initial display when the program is run on bootstrap node  

   ```
   Bootstrap loaded and Initialized.
	 Please provide a command. The possible commands are :
	 VIEW -- VIEW [hostname]
	 INSERT -- INSERT filename
	 SEARCH -- SEARCH filename
   ```

- Initial display when the program is run on the other nodes (hostname\_server2, hostname\_server3 and hostname\_server4)  

   ```
   Please provide a command. The possible commands are :
	 JOIN -- JOIN
	 VIEW -- VIEW [hostname]
   ```

- Joining from hostname\_server2. Display of JOIN success is as shown below,  

   ```
   JOIN SUCCESSUL!
 	 IP of New Peer : hostname_server2/IP_server2
 	 Hostname of New Peer : hostname_server2
 	 Zone of New Peer : (5.0-10.0,0.0-10.0)
   ```

- Viewing from hostname\_bootstrap\_node (VIEW)(this will display information of all the peers in the network)  

   ```
   Hostname : hostname_server2
	 ------------------------------------------------------------------
	 Ip Address : IP_server2
	 Zone : (5.0-10.0,0.0-10.0)
	 Temp Zone : null
	 Files : []
	 Temp files : []
	 Neighbours : hostname_bootstrap_node,
	 ------------------------------------------------------------------
	 Hostname : hostname_bootstrap_node
	 ------------------------------------------------------------------
	 Ip Address : IP_bootstrap_node
	 Zone : (0.0-5.0,0.0-10.0)
	 Temp Zone : null
	 Files : []
	 Temp files : []
	 Neighbours : hostname_server2,
	 ------------------------------------------------------------------
   ```

- Joining from hostname\_server3. Display of JOIN success is as shown below,  

   ```
   JOIN SUCCESSFUL!
   IP of New Peer : hostname_server3/IP_server3
   Hostname of New Peer : hostname_server3
   Zone of New Peer : (5.0-10.0,0.0-5.0)
   ```

- Viewing from hostname\_bootstrap\_node (VIEW)(this will display information of all the peers in the network)  

   ```
   Hostname : hostname_server2
   ------------------------------------------------------------------
   Ip Address : IP_server2
   Zone : (5.0-10.0,5.0-10.0)
   Temp Zone : null
   Files : []
   Temp files : []
   Neighbours : hostname_server3, hostname_bootstrap_node,
   ------------------------------------------------------------------
   Hostname : hostname_server3
   ------------------------------------------------------------------
   Ip Address : IP_server3
   Zone : (5.0-10.0,0.0-5.0)
   Temp Zone : null
   Files : []
   Temp files : []
   Neighbours : hostname_server2, hostname_bootstrap_node,
   ------------------------------------------------------------------
   Hostname : hostname_bootstrap_node
   ------------------------------------------------------------------
   Ip Address : IP_bootstrap_node
   Zone : (0.0-5.0,0.0-10.0)
   Temp Zone : null
   Files : []
   Temp files : []
   Neighbours : hostname_server2, hostname_server3,
   ------------------------------------------------------------------
   ```

- Joining from hostname\_server4. Display of success is as shown below.  

   ```
   JOIN SUCCESSUL!
   IP of New Peer : hostname_server4/IP_server4
   Hostname of New Peer : hostname_server4
   Zone of New Peer : (7.5-10.0,5.0-10.0)
   ```

- Viewing from hostname\_bootstrap\_node (VIEW)(this will display information of all the peers in the network)  

   ```
   Hostname : hostname_server2
   ------------------------------------------------------------------
   Ip Address : IP_server2
   Zone : (5.0-7.5,5.0-10.0)
   Temp Zone : null
   Files : []
   Temp files : []
   Neighbours : hostname_server3, hostname_server4, hostname_bootstrap_node,
   ------------------------------------------------------------------
   Hostname : hostname_server4
   ------------------------------------------------------------------
   Ip Address : IP_server4
   Zone : (7.5-10.0,5.0-10.0)
   Temp Zone : null
   Files : []
   Temp files : []
   Neighbours : hostname_server2, hostname_server3,
   ------------------------------------------------------------------
   Hostname : hostname_server3
   ------------------------------------------------------------------
   Ip Address : IP_server3
   Zone : (5.0-10.0,0.0-5.0)
   Temp Zone : null
   Files : []
   Temp files : []
   Neighbours : hostname_server2, hostname_server4, hostname_bootstrap_node,
   ------------------------------------------------------------------
   Hostname : hostname_bootstrap_node
   ------------------------------------------------------------------
   Ip Address : IP_bootstrap_node
   Zone : (0.0-5.0,0.0-10.0)
   Temp Zone : null
   Files : []
   Temp files : []
   Neighbours : hostname_server2, hostname_server3,
   ------------------------------------------------------------------
   ```

- Inserting filename abc.txt at hostname\_server2. Display of INSERT success message is as shown below.  

   ```
   Command : INSERT
   Status : INSERT operation successful.
   Inserted file : abc.txt.
   Peer hostName : hostname_bootstrap_node.
   Peer ipAddress : hostname_bootstrap_node/IP_bootstrap_node
   Affected Peer hostname : hostname_bootstrap_node
   Affected Peer ipAddress : hostname_bootstrap_node/IP_bootstrap_node
   Affected Peer zone : (0.0-5.0,0.0-10.0)
   Route taken : hostname_server2 -> hostname_bootstrap_node
   ```

- Searching for file from filename from hostname\_server4. Display of SEARCH success message is as shown below.  

   ```
   Command : SEARCH
   Status : Search successful
   Affected Peer hostname : hostname_bootstrap_node
   Affected Peer ipAddress : hostname_bootstrap_node/IP_bootstrap_node
   Affected Peer zone : (0.0-5.0,0.0-10.0)
   Route taken : hostname_server4 -> hostname_server2 -> hostname_bootstrap_node
   ```

- LEAVE request from hostname\_server2. Display of LEAVE success message is as shown below.  

   ```
   Leave Successful
   -----------------
   Hostname of node that left : hostname_server2
   Ip address of node that left : hostname_server2/IP_server2
   ```

- Viewing all the peers' information from hostname\_server3. The display of information of all the peers is as shown below.  

   ```
   Hostname : hostname_server4
   ------------------------------------------------------------------
   Ip Address : IP_server4
   Zone : (5.0-10.0,5.0-10.0)
   Temp Zone : null
   Files : []
   Temp files : []
   Neighbours : hostname_server3, hostname_bootstrap_node,
   ------------------------------------------------------------------
   Hostname : hostname_bootstrap_node
   ------------------------------------------------------------------
   Ip Address : IP_bootstrap_node
   Zone : (0.0-5.0,0.0-10.0)
   Temp Zone : null
   Files : [abc.txt]
   Temp files : []
   Neighbours : hostname_bootstrap_node, hostname_server3,
   ------------------------------------------------------------------
   Hostname : hostname_server3
   ------------------------------------------------------------------
   Ip Address : IP_server3
   Zone : (5.0-10.0,0.0-5.0)
   Temp Zone : null
   Files : []
   Temp files : []
   Neighbours : hostname_server4, hostname_bootstrap_node,
   ```

# Tera_Emulator_v1xxx
This is a WIP[Work in progress].

To copmile this you need:
      -boost code
      -mysql code

In the Config/server.txt you find:
     
      -first line - server's ip
      
      -second line- server's port
      
      -third line-max connected clients
     
      -fourth line - mysql server ip
     
      -fifth line -mysql user 
     
      -sixth line -mysql password
      
      -seventh line - mysql database name

      inventory.bin and deposit.bin are used to save players inventory and deposit items to database asa BLOB.
      Format:each item is writed as an int[4 bytes].

      v1020
      -rsolved some bugs
      -more stabile
      -added future need code
      -max point[login->hit lobby]
      v1025
      -changed Client Recv and Send overall logic.
            -now send and receive are on separated threads
            -Send(byte*,unsigned int) mutexted function, ads ISendPackets to the queue
            -InternalSend(byte*,unsigned int) accessed only by Send thread, encrypts the data and sends it over the network to client
            -receive gets 1 packet processes it and adds packets to be sent to the queue
            -while receive thread -> othre threads may post packets [like chat system...] [NOT TESTED]
            -send thread pops all the elements in the queue [ISendPacket] and InternalSend(s) them.

# CS118 Project 2

This is the repo for Winter 2023 cs118 project 2.

## Names
Daniel Wang, dwangnh@gmail.com, 505572831
Spencer Sang, stsang333@gmail.com, 405485245

## Implementation Details
Client:
After the 3-way handshake, the client immediately sends the remaining (up to 9) packets in its window. For each ACK the client receives, it will move its window (shift all packets in window) until the pkt with the corresponding seqnum is first in the window. This opens up new space in the window for the next packets to be added. In the case of timeout, because only one timer is necessary, only the first packet in the window will ever time out. When that happens, the entire window is retransmitted.

Server:
After the 3-way handshale, the server tracks its next expected packet. If the received packkt is not the next expected packet, the server will send an ack for its next expected packet. It only writes in-order packets to the file.

## Problems
One of the first problems that we ran into was failing to account for the loss of Ack packets. In this case, because of the cumulative ack, the client receiving back an ack of greater value should should consider all packets up until that value as acknowledged.
Another problem we ran into was in reading and writing to the files. Initially we tried using fseek to move the file pointer when trying to perform successive reads/writes. We then realized that fread and fwrite automatically move the file pointer after the function is performed.

## Additional Resources
Only additional resources used were the documentation for certain C functions.

## Makefile

This provides a couple make targets for things.
By default (all target), it makes the `server` and `client` executables.

It provides a `clean` target, and `zip` target to create the submission file as well.

You will need to modify the `Makefile` USERID to add your userid for the `.zip` turn-in at the top of the file.




* curl -v --trace out.txt http://google.com
* Each request split to IP packets having segments and then collected and ordered at server end to receive the complete request
* Journey of a request
  * Accept - When a client connects to a server on port 443, a 3 way handshake is completed by the server OS kernel and the connection is placed on the listener queue, we call this queue the accept queue. The backend application is responsible to invoke syscall accept() on the listener socket to create a file descriptor which represents the connection.
  * Read - Request is series of bytes with a clear start and end defined by the protocol that is used. We have to remembers that those are raw bytes that are encrypted and encoded, there is no request here just bytes, for all we know those bytes we read could be 10 requests or could be half of a request
  * Decrypt - we can’t see any requests or know the boundary of the protocol until we decrypt the content to see the headers and other metadata. This could be HTTP/1.1 or HTTP/2 or even SSH.  Decryption is CPU bound operations, it can be done in its own thread or in same thread as read and accept
  * Parse - we have plaintext readable bytes we can use our knowledge of the agreed upon protocol to parse requests, the chunk of bytes we read might have a full request
  * Decode - Request using JSON or protobuf can be deserialized in this step to objects based on the language of choice. We turn the raw bytes into language structures which has its own cost and memory footprint.
  * Process - Actual request backend process kick in
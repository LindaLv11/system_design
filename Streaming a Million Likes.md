Streaming a Million Likes:

Distribuion of Likes: 

For each connection
    sender -> likes backend (publisher) -> Real-time Delivery system -> receiver:

    Real-time Delivery system -> receiver     needs a persistent connection:

    persistent connection (HTTP long pool server sent events)

    This connections does not disconnect, keep streaming data on the same open connection. 

    Client: HTTP GET request + {event-stream} in the accept header. 
            create {EventSource} object with a target URL
            defines event handlers to process chunk of data



    Server: HTTPs 200 OK + sets the content type to {event-stream}
            streaming chunks of data
            each chunk processed independently on the client through {eventsource} interface

          
For thousands of connections:
 
      manage connetions using Akka
      Akka Actors are objects which have some {state}, and they have some {behavior}.
      {behavior} defines how the state should be modified when they receive certain messages. 
                 how to publish that event to the EventSource connection

      {mailbox}: communicate exclusively by exchanging messages
      {stat} == one persistent connection 

      An actor is assigned a lightweight thread every time there is a message to be processed. 
      That thread will look at the behavior that is defined for the message and modify the state 
      of the Akka Actor based on that definition. 

      Client: connects to the server, assigned connectionID(random)
              AKKA actor to manager connection  (one to one mapping)
              AKKA supervisor actor broadcast to all actors. 


 
Broadcast:
    
    subscribe request 
    In-Memorysubscription table (local, volital)
   
Scale challenge: add machine
  Real-time dispatcher 
  

    
    
    
    

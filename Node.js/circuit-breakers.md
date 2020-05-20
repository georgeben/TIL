#### Circuit breakers
When your Node.js app is made up of different services📦 that communicate with each other, (or even a 3rd party service), there is always a tendency that a service might fail🤒 and will not respond when being called by other services.
When this happens, a service calling the failed service becomes stalled ⏳⏳⏳ (as there is no response from the failed service). While it is stalled, your app might still be receiving requests (maybe thousands) from your users,
which will also be stalled. The error from one service cascades to other services. These stalled requests as a result of one failed service will eventually consume all your computing resources, bringing your whole app down 🔥😭.  
#### Solution?
Use a circuit breaker! A circuit breaker watches your services for failure, if the number of times a service fails consecutively reaches a limit, the circuit breaker disconnects that service for a given timeframe. Within that timeframe, any request
to the failed service will not go through (hence, your application is not stalled) After the timeframe elapses, the circuit breaker allows few requests to the service that was failing, if it fails again, the timeout period starts again, if the 
requests succeed, the app goes back to it's normal behaviour.

The PAVE Vehicle Capture Interface (PAVE) delivers a mobile experience on a user's mobile device without installation, clicking a link opens PAVE using the appropriate installed browser. 

PAVE harnesses the phone's native capabilities to guide the user to capture images of a vehicle at specific angles to collect the vehicle information and allow PAVE to complete a real-time visual inspection of the car.

The API provides a RESTful interface with JSON-formatted response.

# Authentication

*General Idea:*

The developer API uses token based authentication. The API Key found in your PAVE dashboard must be added to the **generate-session-id** POST request url to generate a session-id. The session-id returned is your case identifier and should be stored, as it serves to identify a unique inspection case (there **MUST** be one of these for **each** vehicle being inspected at a given time). That key is then added to the link that lauches PAVE Bot. 

*Important*: The session-id is the only ID you need, you do not need to provide or generate any other id, since the **generate-session-id** request will be generating a unique identifier for you. 


*In Practice:*

PAVE API licence is assigned a universally unique identifier (UUID) API key. This **secret** API key can be found within the **Integrations** tab of the PAVE Dashboard. Make sure to keep this API key on the server side, protected from the client (see **Generate a new API Key**).  
**Each PAVE API licence must have a unique API key**, in other words, each implementation will include a unique API Key.
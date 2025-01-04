# FloatingSketches
A 2D scanner that feeds sketches into a network of pipes that are equipped with displays.

There is a server, a scanner and clients with displays connected to that server.

The API between the server and the clients needs to be well defined so that the client units can be implemented on a variety of different platforms.

We want to provide an Arduino library (and maybe others) implementing this API.


## Client

Find details about the client implementations [here](clients/README.md).

The client shows an underwater environment on its display.

- regularly polls the server for the list of fishes to be displayed on this client
  - this implicitly registers the device at the server
  - the server only stores devices in RAM
- reports to server when a fish left the screen
- loads the necessary image from the servers image endpoint


## Scanner

Find details about the scanner implementation [here](scanner/README.md).

- place drawn picture into scanner
- press button
- scanner takes photo and crops it out (removes white border)
- scanner pushes new image to server
- server ~~crops it out and~~ assigns the new image to first client

TBD: Maybe same binary as server? Like so:

```bash
# both server and scanner
./floatingsketches

# only one of them
./floatingsketches server
./floatingsketches scanner
```


## Server

Find details about the server implementation [here](server/README.md).

The server needs some auditing mechanism for new images before they get distributed to the clients.

The server hosts a web interface. There, the admin can configure the network between registered clients.

The server manages the movement of sketches between the clients along the configured connections.

The server device usually also hosts a WiFi network for the clients and optionally a device using the web interface.

### API Endpoints

#### HTTP

- `GET /api/devices` list all devices (frontend)
- `GET /api/devices/:deviceID` (list fishes on device, add device to selection) (device)
	- HEADER `json` or `CSV`
	- `FishID`, `ImageID`, `(FromDirection/REMOVE)` (remove is emergency remove)
- `DELETE /api/fishes/:fishID/leave/:deviceID?direction=` (device sends a notification to the server)

- `GET /api/fishes` list all fishes (frontend)
- `POST /api/fishes` send image (scanner) + HTTP upload form for debugging
- `GET /api/images/:id?size=` get fish image (frontend & device)
- `DELETE /api/fishes/:id`  API to remove fish -> trigger on all devices remove (frontend)


#### TCP (optional if HTTP is too bulky for embedded devices)

- Client -> Server (idenfitifer)
	- Response: Viele ID;Direction für denn aktuellen State
- Server -> Client (ID;LEFT)
- Client -> Server (ID;RIGHT)
- Server -> Client (ID;REMOVE)



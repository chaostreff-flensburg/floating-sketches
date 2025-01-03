# FloatingSketches
A 2D scanner that feeds sketches into a network of pipes that are equipped with displays.


## System Description

There is a server with a scanner and display connected to that server.

The API between the server and the displays needs to be well defined so that the display units can be implemented with a variety of different platforms.

We want to provide an Arduino library (and maybe others) implementing this API.


### Server

The server scans new sketches that need to be validated by some (preferably fast - e.g. a few seconds) auditing system so that profanity can be blocked.

The server hosts a web interface. There, the admin can add new display to the network and define how those nodes are connected to the server and each other.

The server manages the movement of sketches between the display along the configured connections.

The server hosts a WiFi network for the displays and optinally a device using the web interface.


### Display

The display shows an underwater environment.

When commanded by the server, the display shows sketches floating into view from the provided direction. The path that a sketch takes on the screen as well as in which direction the sketch leaves the view is free to be implemented by the display.

When a sketch has left the view, the display reports this back to the server so that it can forward that sketch to another display connected to the exit direction.



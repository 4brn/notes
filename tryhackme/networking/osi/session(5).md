# Session

> Once data has been translated or formated from the Presentation (6), the session layer will create a connection to the computer that the data is destined for.

When a connection is established, a **session** is created.
The session is active, while there is a connection.

- layer 5 ensures that both computers are on the same page before data is sent.

The data is divided into smaller chunks of data (Packets) and begin sending them **one by one**.
This ensures that if the connection is lost, only the unsent packets will have to be sent again.

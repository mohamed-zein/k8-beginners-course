# Unit 9: Microservices Architecture
In this unit, we will try to understand Microservices Architecture through an example application.
## Sample Application - Voting Application
This is a voting application which provides 2 web interfaces:
1. Web Interface for the user to enter the vote.
2. Web Interface for the user to see the result.
### Application Architecture
The application consists of several components:
* **voting-app**: A web application developed in [Python](https://www.python.org/) to provide the user to choose between 2 options: _CATS_ and _DOGS_.
* **in-memory DB**: A [redis](https://redis.io/) database which stores the user's choise from the **voting-app**.
* **worker app**: An application written in [.NET](https://dotnet.microsoft.com/en-us/) which processes the user's voting record stored in redis **in-memory DB** and update the persistent database.
* **db**: A [PostgreSQL](https://www.postgresql.org/) database which has a table with the number of votes for each category. The **worker app** is responsible for updating this table based on votes registered in the **in-memory DB**.
    CATS | DOGS
    -----|-----
    0 | 1
* **result-app**: A web application written in [Node.js](https://nodejs.org/en/) that displays the results of the votes stored in the [PostgreSQL](https://www.postgresql.org/) database.
The application is built by different tools and different development platforms.


[<<Previous](../unit08-services/README.md) | [Next>>]()
# Bacteria Server

In order to connect your local database to the project, copy `database.example.yml` from
`config/database.example.yml` to `config/database.yml` and insert your own username and password credentials
from your local postgres database

### General overview of the Bacteria War Game

We have a two dimensional map as our battlefield for bots. For example 300x300. Map should contain walls through which Bacterias can not pass. In predefined places in the corners, corresponding to 4 teams which will be involved in the game, will appear 10 bacterias. Each Bacteria can:

- Move top, right, bottom, left with exactly one cell of the grid.
- View of each Bacteria is limited to one cell of the grid.
- Bacteria can eat sugar at one cell distance to it.
- More bacterias can be on the same position of the grid at the same time.

The sugar which is the target of the game will appear randomly on the map. When a bacteria eats sugar another piece appear after 3 time periods of the game. The winner of the game is the bot which eats the most amount of sugar in predefined amount of time periods. (For example: 400 iterations) Each time period involves:

- Move of each individual bacteria on the map.
- New sugar to appear in case one was eaten.

### Sever is responsible for.

- Basic API of the game.
- Generating a game tick with predefined frequency (Example: 1s).
- Hardcoded map of the Bacteria game.
- Generate sugar on the game grid.
- Respond to each of the clients with updated information of the map.
- Aggregate 4 requests(corresponding to each player) with their actual move for each of the Bacteria on the map.

### Client is responsible for.

Basic API consume for sending data about its move and getting updates of the current state of the map. (GET, POST).
1) Sending data about: each cell move.
2) Receiving data about: each cell view.(What can see each Bacteria)

Client should implement its own algorithm of how cell will behave depending of what they see. (Avoiding move cell corresponding to wall, eating sugar)

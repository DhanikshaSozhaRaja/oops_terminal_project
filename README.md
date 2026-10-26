# Scrabble Game in C++

## 1. About the Project

This project is a C++ implementation of the classic Scrabble word game. The main idea is to allow players to form words using letter tiles, earn points based on the letters and board positions, and compete to achieve the highest score.

We developed the project by dividing the work among four members. Each member was responsible for a different part of the game, such as tile management, the game board, word validation and scoring, or the main game flow.

The current version provides a terminal-based interface. The project is structured so that a graphical interface can be added in a future version without rewriting all the game logic.

## 2. Objectives

- Develop a playable Scrabble game using C++.
- Implement the board, letter tiles and player racks.
- Validate words using a dictionary.
- Calculate scores based on letter values and premium squares.
- Support multiple players taking turns.
- Handle tile exchanges, passing turns and game completion.
- Keep the game logic separate from the user interface to make future improvements easier.

## 3. Technologies Used

- **Programming Language:** C++
- **C++ Standard:** C++17
- **Build System:** CMake
- **Compiler:** GCC or another compatible C++17 compiler
- **Interface:** Terminal-based interface
- **Data:** Text-file dictionary
- **Testing:** C++ test program and CTest

The current terminal version does not require SFML. SFML can be used for the graphical version described in the original project plan.

## 4. Work Division Among Team Members

### Member 1 – Tile Management and Player System

Member 1 is responsible for handling the letter tiles and player-related functionality.

Main responsibilities:
- Creating and managing individual letter tiles.
- Maintaining the tile bag and its letter distribution.
- Drawing tiles from the bag and returning or exchanging tiles.
- Managing each player's rack.
- Adding and removing tiles from a player's rack.
- Keeping track of player scores and remaining tile points.

These components provide the basic resources needed for players to participate in the game.

### Member 2 – Game Board and Placement Rules

Member 2 is responsible for implementing the Scrabble board and checking whether tiles can be placed correctly.

Main responsibilities:
- Creating the 15 × 15 game board.
- Managing individual board cells.
- Representing normal and premium scoring squares.
- Checking whether a word placement is valid.
- Ensuring the first word covers the centre square.
- Checking connections with existing words.
- Committing valid tile placements to the board.
- Testing board placement rules and game scenarios.

This module ensures that players follow the basic board placement rules.

### Member 3 – Dictionary, Scoring and Supporting Components

Member 3 is responsible for word validation, score calculation and supporting components.

Main responsibilities:
- Loading words from a dictionary file.
- Checking whether submitted words exist in the dictionary.
- Calculating scores using letter values and premium squares.
- Applying the bonus for using all seven rack tiles.
- Managing high-score records.
- Maintaining shared build configuration and test utilities.
- Preparing supporting interface components and resources for the planned graphical version.

This module helps ensure that words are checked and points are calculated consistently.

### Member 4 – Game Logic, Main Program and Integration

Member 4, Dhaniksha, is responsible for connecting the individual components and managing the overall game flow.

Main responsibilities:
- Initialising the game and player turns.
- Distributing tiles to players at the start of the game.
- Connecting the player, board, dictionary and scoring components.
- Processing word submissions and handling invalid moves.
- Managing passing and exchanging tiles.
- Updating scores and determining when the game ends.
- Integrating high-score functionality.
- Creating and testing the main program.
- Planning the graphical game window and its interaction with the game logic.

In the current terminal version, this role also involves connecting the commands entered by the user to the underlying game engine.

## 5. Features of the Current Version

The terminal version includes the following features:

- Support for 2–4 local players.
- A 15 × 15 Scrabble board.
- Letter tiles with assigned point values.
- Dictionary-based word validation.
- Horizontal and vertical word placement.
- Board placement validation, including the opening centre-square rule.
- Letter and word multipliers.
- A 50-point bonus for using all seven tiles in one move.
- Passing a turn and exchanging tiles.
- Player score tracking.
- Endgame scoring.
- Saving high-score records to a file.

Some advanced official Scrabble rules, including blank tiles and challenge rules, are not implemented in this basic version.

## 6. Project Structure

```text
scrabble_terminal/
├── CMakeLists.txt
├── README.md
├── run_windows.bat
├── include/
│   └── scrabble.hpp
├── src/
│   ├── main.cpp
│   └── scrabble.cpp
├── data/
│   └── dictionary.txt
├── tests/
│   └── test_scrabble.cpp
├── docs/
│   └── DESIGN.md
└── build/
```

**Folder descriptions:**

- `include/` contains the shared declarations used by the game.
- `src/` contains the main program and game implementation.
- `data/` contains the dictionary used for word validation. High-score data is generated when the game saves scores.
- `tests/` contains the test program.
- `docs/` contains design documentation.
- `build/` contains generated build files and the compiled executable. It is created during the build process.

The current terminal implementation combines the core logic into a small number of files. The four-member division above describes the logical responsibilities from the team plan, rather than claiming that every member already has a separate source file in this version.

## 7. How to Build and Run

### Requirements

Install:
- A C++17-compatible compiler.
- CMake.
- A suitable build tool, such as Ninja or the Visual Studio C++ build tools.

### Build using CMake

Open a terminal in the project directory and run:

```bash
cmake -S . -B build
cmake --build build
```

Run the tests:

```bash
ctest --test-dir build --output-on-failure
```

On Windows, if the project was built using the Ninja generator, start the game with:

```powershell
.\build\scrabble.exe
```

If using a Visual Studio generator, the executable will generally be located under `build\Debug\scrabble.exe` for a Debug build.

## 8. How to Play

1. Start the executable.
2. Enter the number of players.
3. Enter each player's name.
4. View the board and the current player's rack.
5. Enter a command to play a word, pass the turn, exchange tiles or view the board.
6. Continue taking turns until the game ends.

### Available Commands

| Command | Purpose |
|---|---|
| `PLAY <row> <column> <H/V> <word>` | Place a word horizontally or vertically |
| `BOARD` | Display the board |
| `PASS` | Pass the current turn |
| `EXCHANGE <letters>` | Exchange selected letters, when permitted |
| `HELP` | Display command instructions |
| `QUIT` | Exit the game |

Example:

```text
PLAY 8 H H HIT
```

This attempts to place `HIT` horizontally, beginning at row 8, column H. The first word must cover the centre square.

## 9. Testing

Testing is used to check that the main parts of the game work as expected.

The project test program checks selected game behaviours, while CTest provides a convenient way to run the tests after building.

Important areas to test include:
- Tile distribution and rack management.
- Valid and invalid word placements.
- Opening moves and board boundaries.
- Dictionary validation.
- Score calculation and premium squares.
- Passing turns and exchanging tiles.
- Endgame scoring and high-score saving.

The current test suite is a basic starting point. Additional tests are needed to cover more complex word intersections and edge cases.

## 10. Limitations

The current version focuses on providing a simple playable Scrabble game. It does not implement every official tournament rule.

Current limitations include:
- No graphical game window in the terminal version.
- No blank tiles.
- No challenge system for disputed words.
- Limited automated coverage of advanced rule combinations.
- The dictionary determines which words are accepted, so its contents affect validation.

## 11. Future Improvements

The project can be extended in several ways:

- Add an SFML-based graphical interface.
- Allow players to drag and drop tiles.
- Add buttons for submitting words, recalling tiles, passing and exchanging.
- Improve error messages and display score details.
- Add more comprehensive automated tests.
- Improve game history and high-score presentation.
- Implement additional official Scrabble rules.

Separating the game logic from the interface makes these improvements easier to introduce without rebuilding the entire project.

## 12. Conclusion

This project helped us understand how to build a small game in C++ by dividing it into manageable components. Tile management, board validation, dictionary checking, scoring and game control all contribute to the final experience.

The terminal version provides a foundation for learning and testing the core game mechanics. With further testing and a graphical interface, it can be developed into a more complete and user-friendly Scrabble game.

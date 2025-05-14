
# Software Requirements Specification (SRS)

## 1. Introduction

### 1.1 Purpose
This Software Requirements Specification (SRS) outlines the design and technical implementation plan for a basic MVP (Minimum Viable Product) of the classic board game **LUDO**, developed using C++ with a GUI framework suitable for Windows (such as **SFML** or **Qt**).

### 1.2 Intended Audience and Reading Suggestions
- Developers familiar with Object-Oriented Programming (OOP) in C++
- Stakeholders interested in the implementation of the MVP version of LUDO
- QA engineers for understanding functional specifications

### 1.3 Scope
The LUDO MVP aims to recreate the core mechanics of the traditional 4-player board game, with support for:
- 4 color tokens: **Red, Green, Yellow, Blue**
- Turn-based movement
- Dice roll simulation
- Basic movement and kill logic
- GUI interface showing the board, dice, and tokens

### 1.4 Definitions, Acronyms, and Abbreviations
- MVP: Minimum Viable Product
- GUI: Graphical User Interface
- SFML: Simple and Fast Multimedia Library
- Qt: A popular cross-platform GUI toolkit for C++

## 2. Overall Description

### 2.1 Product Perspective
The product is a standalone desktop game, developed entirely in C++ using OOP principles and a GUI library (e.g., **SFML** or **Qt Widgets**). It will run on Windows systems.

### 2.2 Product Features
- Graphical representation of LUDO board
- 4 sets of colored tokens (4 each for Red, Green, Yellow, Blue)
- Interactive dice roll
- Automatic turn switching
- Basic kill logic (when a token lands on an opponent's token)

### 2.3 User Classes and Characteristics
- **Players (Users):** Casual users interested in playing LUDO on PC

### 2.4 Operating Environment
- OS: Windows 10/11
- Language: C++17 or newer
- GUI Library: SFML 2.6.x / Qt 6.x

### 2.5 Design and Implementation Constraints
- No online multiplayer support in MVP
- Single machine use only
- No AI; only manual user control

### 2.6 Assumptions and Dependencies
- Players are familiar with LUDO rules
- Only four players (colors) supported, all human-controlled

## 3. System Features

### 3.1 Game Board Display
**Description:** Renders the LUDO board with home zones, safe paths, and colored bases.

**Functional Requirements:**
- FR1.1: Display board with correct layout and scaling
- FR1.2: Color-code areas (Red, Green, Yellow, Blue)
- FR1.3: Show 4 tokens per player

### 3.2 Dice Roll Mechanism
**Description:** Allows players to roll a virtual dice by clicking a button.

**Functional Requirements:**
- FR2.1: Generate a number between 1 to 6
- FR2.2: Animate dice roll on screen
- FR2.3: Pass control to player based on dice outcome

### 3.3 Token Movement
**Description:** Tokens move based on dice result along predefined paths.

**Functional Requirements:**
- FR3.1: Allow selection of movable tokens
- FR3.2: Animate token movement along path
- FR3.3: Validate movement legality

### 3.4 Token Capture (Kill)
**Description:** A player's token captures another if it lands on it (unless in a safe zone).

**Functional Requirements:**
- FR4.1: Detect collisions of tokens
- FR4.2: Reset captured token to base

### 3.5 Turn Management
**Description:** Turns change in clockwise order unless player rolls a 6.

**Functional Requirements:**
- FR5.1: Cycle turns between players
- FR5.2: Allow extra turn on dice roll of 6

## 4. External Interface Requirements

### 4.1 GUI Interface
- Main Window
- Board Display
- Dice Display
- Token Movement
- Turn Indicator

### 4.2 Performance Requirements
- Low memory usage
- Smooth animation at ~60 FPS (if using SFML)

## 5. Non-Functional Requirements

### 5.1 Usability
- Simple interface
- Clear visual feedback for turns and movement

### 5.2 Reliability
- No crashes on illegal moves
- Proper turn enforcement

### 5.3 Maintainability
- Well-structured C++ classes
- Modular architecture with separate classes for GameManager, Player, Token, Board, Dice

### 5.4 Portability
- Initially for Windows only, but codebase should allow portability to Linux with GUI changes

## 6. Class Structure Overview (C++)

### 6.1 Classes
```cpp
class GameManager {
  void startGame();
  void nextTurn();
  void handleDiceRoll();
};

class Player {
  Color color;
  std::vector<Token> tokens;
  void playTurn(int diceRoll);
};

class Token {
  int position;
  bool isAtHome;
  void move(int steps);
  void resetToBase();
};

class Dice {
  int roll();
};

class Board {
  void render();
  Position getNextPosition(Token, int);
};
```

## 7. Tools and Technologies
- **Programming Language:** C++
- **GUI Library:** SFML (preferred for simpler MVP) or Qt (for richer GUI)
- **IDE:** Visual Studio / CLion
- **Version Control:** Git

## 8. Future Enhancements
- Add AI opponents
- Multiplayer support (LAN/Online)
- Score tracking and leaderboards
- Save/load game states

---

> **Note:** For MVP, SFML is preferred due to ease of drawing 2D graphics and handling basic input. If you prefer drag-and-drop GUI design, Qt is better, though it has a steeper learning curve.

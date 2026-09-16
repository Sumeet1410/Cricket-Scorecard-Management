# Cricket Scorecard Management

A Java console application designed to manage, simulate, and record cricket matches. It handles team setups, toss outcomes, ball-by-ball score tracking (including extras, wickets, and strike rotation), and exports a detailed match scorecard to a file.

---

## Features

- **Team & Player Setup**: Configure two teams with 6 players each and specify the venue/stadium.
- **Automated Toss**: Simulates coin toss and automatically assigns batting and bowling sides.
- **Match Simulation (6 Overs / Innings)**:
  - Ball-by-ball scoring system.
  - **Runs (0–6)**: Updates striker stats, team score, bowler figures, and rotates strike on odd runs.
  - **Wickets (`7`)**: Records dismissals, updates bowler stats, advances batting order, and declares "All out" on 5 wickets.
  - **Wides (`8`)**: Grants 1 run to the batting team without counting as a legal delivery.
  - **No-Balls (Negative values)**: Penalizes bowler, awards runs, rotates strike if needed, and repeats the ball.
  - **Strike Rotation**: Automatically rotates batsman strike at the end of each over and on odd runs.
  - **Target Chase Logic**: Detects when the chasing team wins the match and concludes the innings.
- **Persistent Scorecard**: Generates and writes complete batting and bowling summaries into [`scorecard.txt`](file:///scorecard.txt).

---

## Class Architecture (OOP Design)

The project demonstrates core Object-Oriented Programming (OOP) principles including Abstraction, Inheritance, Interfaces, and Encapsulation:

| Component | Type | Description |
| :--- | :--- | :--- |
| `Scorable` | `interface` | Defines common scoring methods (`addRuns`, `addBallFaced`, `addWicket`, `addover`, `addRunsgiven`). |
| `CricketMatch` | `abstract class` | Base class defining match properties (`team1`, `team2`, `stadium`, `tossWinner`) and abstract methods (`conductToss`, `startMatch`). |
| `Player` | `class` | Implements `Scorable`; encapsulates individual batting, bowling, overs, and strike-rate metrics. |
| `Team` | `class` | Represents a team, holding the roster list, total runs, and wickets lost. |
| `CricketScorecard` | `class` | Extends `CricketMatch`; contains match engine, ball evaluation loop, and scorecard export. |
| `CricketScorecardManagement` | `public class` | Application entry point containing `public static void main(String[] args)`. |

---

## Scoring Input Guide

During the match, input the outcome of each ball into the terminal:

| Input | Meaning | Action |
| :---: | :--- | :--- |
| `0` - `6` | Normal runs | Adds runs to batsman & team; strike rotates on odd runs. |
| `7` | Wicket | Striker dismissed; next batsman takes the crease. |
| `8` | Wide ball | 1 extra run added; ball re-bowled. |
| `-N` (e.g. `-4`) | No-ball with runs | Awards `N` runs, repeats ball, rotates strike if odd runs. |

---

## How to Compile and Run

### Prerequisites
- Java Development Kit (JDK 8 or later) installed.

### Compilation
Open a terminal in the project directory and compile:
```bash
javac CricketScorecardManagement.java
```

### Execution
Run the application:
```bash
java CricketScorecardManagement
```

After the match concludes, open [`scorecard.txt`](file:///scorecard.txt) to view the generated match scorecard.
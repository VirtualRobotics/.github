# Project: VirtualRobotics Simulation Platform
## Overview

This project is a simulation platform for testing autonomous navigation and Computer Vision (CV) algorithms. It decouples the physical simulation from the algorithmic logic:

    Unity (Client): Handles physics, rendering, and the "virtual robot" agent.

    Python (Server): Processes camera images from the robot and decides movement logic (CV & RL).

The goal is to test algorithms in a safe, randomized environment without expensive hardware.
## Architecture & Repositories

The project consists of two separate repositories that must run simultaneously:

    VirtualRobotics-Unity: The visualization engine.

    VirtualRobotics-Server: The backend logic (Computer Vision/ML).

Logic Flow:

    Unity sends a camera frame to Python.

    Python processes the image.

    Python sends a movement command back to Unity.

## Prerequisites

Before running, ensure you have:

    Unity Hub (and the compatible Editor version).

    Python 3.x installed.

    uv: An extremely fast Python package installer and runner.

## Getting Started (Step-by-Step)

Follow this specific order to avoid connection errors.
1. Start the Python Server

The server must be listening before Unity attempts to connect.

    Navigate to the VirtualRobotics-Server root directory.

    Run the server using uv:
    Bash

    uv run main.py

    Wait for the console to indicate the server is listening (e.g., Waiting for connection...).

2. Start the Unity Simulation

    Open Unity Hub.

    Click Add -> Add project from disk.

    Select the VirtualRobotics-Unity folder.

    Open the project and press the Play (▶) button at the top.

## Simulation Modes (Main Menu)

Once Unity is running, you will see a Main Menu with three options:
1. O projekcie (About)

    Displays project information, credits, and usage instructions.

2. Start: Heurystyka (Heuristic Mode)

    Logic: Uses classical CV/algorithms to solve the maze.

    Goal: Find and touch the Red Cube.

    Reset Condition:

        The agent touches the Red Cube.

        The user presses the RESET button manually.

    Behavior: On reset, the maze is randomly regenerated, and the agent returns to the start.

3. Start: AI Learning (RL Mode)

    Logic: Uses Reinforcement Learning (RL) to navigate.

    Goal: Find and touch the Red Cube.

    Reset Condition:

        The agent touches the Red Cube.

        Time Limit: 60 seconds pass without success.

        The user presses the RESET button.

    Behavior: Auto-regenerates the maze and resets the agent position upon any of the conditions above.

6. Troubleshooting / Common Issues

    Connection Refused: Ensure uv run main.py is running before you press Play in Unity.

    Firewall: If the repositories are on different machines (rare), allow traffic on the specified port.

    Dependencies: If uv fails, check pyproject.toml or requirements.txt in the server repo.

## TL;DR

    Architecture: Unity handles graphics/physics; Python handles the brain/CV.

    Run Order: Run Python (uv run main.py) first, then press Play in Unity.

    Modes: "Heurystyka" (Manual reset/Goal reset), "AI Learning" (Auto-reset after 60s).

    Resets: Every reset regenerates a completely new random maze.

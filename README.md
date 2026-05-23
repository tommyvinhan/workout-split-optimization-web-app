# Workout Optimization App

## Overview

This project is an interactive workout optimization application that generates structured weekly workout schedules using mixed-integer linear programming. The goal is to help users create a realistic and balanced workout plan without manually sorting through hundreds of exercises.

The model builds a 6-day workout split using a large exercise catalog while considering exercise ratings, workout time, muscle-group balance, recovery spacing, and weekly training frequency. The final application is deployed as a Streamlit web app.

## Live App

https://da353-workoutoptimization.streamlit.app

## Project Motivation

Many people struggle to build effective workout plans because gyms offer a large number of possible exercises, machines, equipment types, and training styles. Choosing the right exercises while balancing muscle groups, recovery, and time can quickly become confusing.

This project solves that problem by treating workout planning as an optimization problem. Instead of selecting exercises manually, the model chooses exercises that maximize workout quality while still following realistic training constraints.

## Data Source

This project uses the Mega Gym Dataset from Kaggle. The dataset contains more than 2,900 exercises and provides structured information about each movement.

Key variables include:

- Exercise title
- Exercise description
- Exercise type
- Body part
- Equipment required
- Difficulty level
- Exercise rating

The rating variable is used as the main quality score in the optimization model. Higher-rated exercises are treated as more valuable and are prioritized when the model builds the workout schedule.

## Data Preparation

Before optimization, the dataset was cleaned and transformed into a format that could be used by the model.

Each exercise was assigned an estimated time cost. The project assumes:

- 3 sets per exercise
- 45 seconds of work per set
- 90 seconds of rest between sets
- About 6 to 7 minutes total per exercise

This time estimate allows the model to compare exercise quality against the limited time available in a workout session.

Exercises were also categorized by training function, including:

- Compound movements
- Isolation movements
- Push exercises
- Pull exercises
- Leg-focused exercises

These categories help the model create a balanced Push-Pull-Legs workout structure.

## Optimization Model

The workout scheduler is formulated as a mixed-integer linear programming problem.

The model uses binary decision variables to decide whether an exercise should be assigned to a specific workout day.

The objective is to maximize the total exercise rating across the weekly workout plan.

In simple terms, the model tries to choose the highest-quality exercises while still respecting practical training rules.

## Constraints

The model includes several constraints to make the workout plan realistic:

- Each workout must stay within a 90-minute time limit
- Each workout day must include a reasonable number of exercises
- Major muscle groups must be trained at least twice per week
- Minor muscle groups must be trained at least once per week
- A muscle group cannot be trained on consecutive days
- Each exercise can appear at most once per week
- Daily volume is capped to avoid overtraining
- The schedule must support a Push-Pull-Legs structure

These constraints help ensure that the generated plan is not only mathematically optimal, but also practical for real training.

## Results

The model generates a 6-day Push-Pull-Legs workout schedule.

The general structure is:

- Push Day A
- Pull Day A
- Leg Day A
- Push Day B
- Pull Day B
- Leg Day B

Push days focus on chest, shoulders, and triceps.

Pull days focus on back, biceps, and pulling movements.

Leg days focus on quadriceps, hamstrings, glutes, calves, and lower-body strength.

The model also creates A and B variations so the user gets variety throughout the week while still training each major muscle group consistently.

## Example Exercises Selected

Examples of exercises selected by the model include:

- Barbell Bench Press
- Incline Dumbbell Press
- Overhead Shoulder Press
- Lateral Raises
- Triceps Pushdown
- Pull-ups
- Barbell Deadlift
- Bent Over Barbell Row
- Barbell Curl
- Barbell Squat
- Leg Press
- Romanian Deadlift
- Standing Calf Raises

These exercises were selected because they satisfy the model constraints while contributing strong ratings and balanced muscle coverage.

## Interactive Application

The optimization model was implemented as a Streamlit application. The app allows users to generate workout plans through a simple interface without needing to understand the mathematical model behind it.

The app demonstrates how prescriptive analytics can be turned into a practical decision-support tool. Users can generate structured workout plans based on training goals, fitness level, and available equipment.

## Tools and Technologies

- Python
- Streamlit
- Pandas
- Mixed-Integer Linear Programming
- Optimization Modeling
- Kaggle Dataset

## Repository Files

- `app.py` — Main Streamlit application
- `solver.py` — Optimization model and workout scheduling logic
- `requirements.txt` — Python dependencies
- `megaGymDataset.csv` — Exercise dataset
- `DA-353-Final-Report.pdf` — Full written project report
- `README.md` — Project documentation

## How to Run Locally

Install the required packages:

```bash
pip install -r requirements.txt

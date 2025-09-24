# COTS UE for AERPAW (Exploring Alternatives)

This README provides an overview of setting up and running a COTS UE (Commercial Off-The-Shelf User Equipment) for AERPAW (Aerial Experimentation and Research Platform for Advanced Wireless).

## Prerequisites

Before running the Open5GS container, two SIM programming commands need to be executed:
1. Opencells SIM programming
2. Pysim SIM programming

These commands set up the necessary parameters for the SIM card to work with the system.

## Configuration Check

It's crucial to verify the `dnn` parameter in the Open5GS config file. This parameter should match the `APN` of the SIM card. The config file is located at `/opt/open5gs/build/configs/open5gs_nr_core_oai.yaml`.

## Running the System

The process involves several steps:

1. Starting the Docker container with specific privileges and network settings.
2. Initiating a TMUX session and starting Open5GS using a helper script.
3. Adding SIM parameters to the Open5GS database.
4. Opening a second TMUX session to start the gNB (gNodeB).
5. Running network performance tests using specific apps.

## Performance Testing

The setup includes running network performance tests. The results are visualized through traffic graphs and charts, showing different bandwidth scenarios (20M, 50M, 100M).

# Simple TCP Implementation in C

This repository contains a C implementation of a simplified Transmission Control Protocol (TCP), built from scratch. The project focuses on the fundamental concepts of reliable data transfer and congestion control, providing a practical understanding of how TCP achieves robustness in network communication.

## Overview

This implementation provides a working example of a simplified TCP protocol, demonstrating how reliable data transfer and congestion control mechanisms can be built using C and UDP.  It handles packet loss, out-of-order delivery, and network congestion, offering a clear view into the core workings of TCP.

## Features

* **Reliable Data Transfer:** Ensures reliable data delivery through acknowledgments, retransmissions, and sequence numbering.  Handles packet loss and out-of-order delivery effectively.
* **Fixed Window Size:** Employs a fixed window size of 10 packets for sending data, managing the amount of data in flight.
* **Cumulative Acknowledgements:**  Uses cumulative ACKs to efficiently acknowledge received packets and signal any missing data.
* **Single Retransmission Timer:**  Manages retransmissions using a single timer for the oldest unacknowledged packet, simplifying the timeout mechanism.
* **Go-Back-N Inspired Retransmission:** Upon timeout, retransmits only the oldest unacknowledged packet, similar to the Go-Back-N protocol, but not identical.
* **Congestion Control:** Implements congestion control mechanisms inspired by TCP Tahoe, including slow start and congestion avoidance.  Dynamically adjusts the congestion window (CWND) based on network conditions.
* **Dynamic RTO Calculation:**  Calculates the Retransmission Timeout (RTO) dynamically based on Round Trip Time (RTT) estimation, using Karn's algorithm and exponential backoff. This ensures adaptive timeout values in varying network conditions. Initial RTT is set to 0 seconds, initial RTO is 3 seconds, and a maximum RTO of 240 seconds is enforced.
* **Fast Retransmit:** Implements fast retransmit, triggering a retransmission upon receiving three duplicate ACKs, which indicates a likely packet loss. (Fast recovery is not implemented).
* **CWND Tracking and Visualization:** Records CWND values over time and saves them to a "CWND.csv" file.  The included `plot` script allows for visualizing the CWND changes, providing insights into the congestion control behavior.


## Implementation Details

* **Language:** C 
* **Transport Layer:** Built on top of UDP for simplicity and to highlight the implementation of TCP features.
* **Network Emulator:** Designed to be tested with the MahiMahi network emulator to simulate various network conditions.
* **Sequence/ACK Numbers:** Uses byte-based sequence and acknowledgment numbers for precise tracking of data.
* **Simplified Model:**  Excludes some TCP features like the three-way handshake, flow control, fast recovery, and delayed ACKs to focus on core concepts.



## Usage

1. Compile the code using the provided Makefile: `make`
2. Start the receiver:  `./rdt_receiver <receiver_port> <output_filename>`
3. Start the sender: `./rdt_sender <sender_port> <receiver_port> <filename>`


**Note:**  The receiver must be started *before* the sender.


## File Structure

* `common.c`: Implementation of common functionalities.
* `common.h`: Header file for `common.c`.
* `Makefile`: Makefile for compiling the code.
* `packet.c`: Implementation related to packet handling.
* `packet.h`: Header file for `packet.c`.
* `plot`: Python script for plotting CWND data (requires `matplotlib`).
* `rdt_receiver`: Executable for the receiver.
* `rdt_sender`: Executable for the sender.
* `README.md`: This file.

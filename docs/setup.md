---
title: Experimental Setup
layout: default
nav_order: 1
---

# Experimental Setup

This documentation describes the components and functionality of the experimental setup used for automated behavioral training in the Mouse Village system. It includes details on the operant chamber, the automated sorting system, and the integration with additional technologies.

---

## Overview

The experimental setup is composed of two main parts:

- **Operant Chamber**: A custom-built chamber designed to conduct behavioral experiments using a touchscreen and reward delivery system.
- **Mouse Village**: An automated training platform that integrates the operant chamber with home cages, enabling 24/7 self-training and remote monitoring.

This setup provides a controlled environment for behavioral research and minimizes human intervention, ensuring consistent training conditions.

## Operant Chamber

The operant chamber is a custom-made structure constructed of white methacrylate. It features two triangular areas connected by a rectangular corridor. The chamber is elevated 20 cm to prevent mice from exiting the platform. The chamber components are described below:

### Physical Structure

- **Main Areas**: The chamber has two opposed triangular areas:
  - **Large triangular area**: Houses an infrared touchscreen used to display stimuli and record responses.
  - **Small triangular area**: Contains a reward delivery port for water reward distribution.

- **Connecting Corridor**: A rectangular corridor equipped with infrared beams to detect the animal’s position.

- **Elevated Platform**: The platform is elevated to avoid immediate walls at the edges, ensuring clear visibility of the touchscreen from all parts of the chamber.

### Touchscreen and Mask

- **Touchscreen**: A 40 x 25 cm infrared touchscreen (ePanel Closed 19” EOS Ibérica) displays visual stimuli.
- **Mask**: A black mask with 4x4 cm holes is placed over the touchscreen. The number of holes can be adjusted according to different task variations, specifying possible stimulus locations.

### Reward Delivery System

- **Reward Port**: Positioned 52 cm from the screen in the small triangular area. Delivers water rewards controlled by the software.

### Detection and Control

- **Infrared Beams**: Placed along the corridor to detect the mouse's body position.
- **Motorized Transparent Door**: Blocks access to the larger area in certain task variations.
- **Piezoelectric Buzzer**: Emits auditory cues based on the mouse's responses.

### Containment and Safety

- **Methacrylate Walls**: Two 60 x 50 cm walls are installed to prevent mice from escaping. The walls are positioned to allow visual access to the screen.
- **Sound-attenuating Box**: The chamber is housed inside a 90 x 70 x 80 cm box, equipped with a fan, overhead lighting, and an infrared camera for monitoring.

### Software Control

- The chamber is controlled by **pyVillage**, a custom-made software developed in Python, which is based on the open-source Bpod State Machine (Sanworks).

## Mouse Village

The Mouse Village is an automated training platform that integrates the operant chamber with the home cage through a tunnel equipped with an RFID-based sorting system. This system enables individualized training and monitoring without human intervention.

### Components

- **Home Cage**: Contains RFID-tagged mice housed in a group.
- **Connecting Tunnel**: Links the home cage to the operant chamber. The tunnel is equipped with:
  - **RFID Sensor**: Detects mice entering the tunnel.
  - **Motorized Doors**: Controls access to the operant chamber and home cage.
  - **IR Camera**: Monitors mouse position and activity.
  - **Scale**: Weighs the mouse before and after training.

### Automated Sorting System

- **Initial State**: Door 1 (near home cage) is open, and Door 2 (near operant chamber) is closed.
- **Mouse Detection**: When a mouse approaches Door 2, the RFID sensor detects it, and if no other mouse is present in the corridor (verified by video tracking), Door 1 closes, and Door 2 opens.
- **Training Session**: The mouse enters the operant chamber, and Door 2 closes until the session is completed.
- **Exit and Weight Measurement**: After the session, Door 2 opens, and the mouse exits. The scale registers the mouse’s weight, triggering Door 2 to close and Door 1 to reopen, allowing the mouse to return to the home cage.

### PyVillage Software Integration

- **Task Scheduling**: PyVillage controls the corridor sorting system and manages remote services. It integrates data from the video-tracking camera and an Arduino microcontroller.
- **Data Management**: After each session, data from Bpod is added to a global dataframe. The mouse-specific parameter dictionary is updated to adjust training difficulty based on the animal’s performance.

### Monitoring and Alerts

- The system is equipped with webcams for remote monitoring.
- Alarms are sent via Telegram to notify researchers in real-time, ensuring continuous supervision of animal behavior and system status.

## Eco-HAB Integration

In some animal groups, the Mouse Village is integrated with **Eco-HAB**, an RFID-based system that tracks voluntary behavior in group-housed mice. This integration allows researchers to record social and environmental preferences, enhancing the scope of behavioral studies.

## Adaptation for Rats

Collaborators from Alex Taylor's Lab at UAB have adapted the Mouse Village platform to train rats in the multiple-choice delayed response task. They utilized the same components and software but scaled the operant chamber to accommodate the dimensions and needs of rats.

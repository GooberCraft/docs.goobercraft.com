---
layout: default
title: Status Plugin
parent: Plugins & Tools
nav_order: 1
permalink: /docs/plugins/status-plugin/
last_modified_at: 2025-11-02
---

## Commands

| Command | Description |
|---------|-------------|
| `/status clear` | Clear your status |
| `/status help` | View the help menu |
| `/status list [availabilities\|statuses]` | Get a list of statuses and availabilities |
| `/status nosleep` | Toggle prompting players to not sleep |
| `/status set <status> <availability>` | Set your status |
| `/status view <username` | View the status of someone |

## Status Indicator

The status indicator is a box next to a players name that has two halfs that indicate a players status and availability. Below you will find the current statues and availabilities confiugured on the server.

_Note: Colors not an exact match to in-game._

### Statuses

| Left Indicator | Status | Description |
|----------------|--------|-------------|
| (Grey) | None | No Status Set |
| (Red) | Busy | Busy with something else |
| (Yellow) | Multitasking | This person is multitasking with other things |
| (Purple) | Streaming | This person is streaming content |
| (Pink) | Recording | This person is recording content |
| (Green) | Playing | This person is just playing the game |

### Availabilities

| Right Indicator | Status | Description |
|-----------------|--------|-------------|
| (Grey) | None | No Availability Set |
| (Green) | Open | This person is open to collaboration |
| (Red) | DoNotDisturb | This person does not want to be disturbed |

### Example

![Status indicator box showing left and right halves with different colors](/assets/images/StatusIndicator.png)

## No Sleep

This plugin also has the ability to let others know that you don't want to sleep through the night. If you run the command `/status nosleep`, when a player enters a bed, a message will appear letting them know you don't want them to sleep.

### Example

![No Sleep notification message in chat](/assets/images/NoSleep.png)

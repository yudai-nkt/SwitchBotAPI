# SwitchBot API Documentation
## Introduction
This document describes a collection of SwitchBot API methods, examples, and best practices for, but not limited to, IoT hobbyists, developers, and gurus to make their own smart home programs or applications. 

## Getting Started
Please follow these steps,
1. Download the SwitchBot app on App Store or Google Play Store
2. Register a SwitchBot account and log in into your account
3. Generate an Open Token within the app (release date to be announced)
4. Roll up your sleeves and get your hands dirty with SwitchBot OpenAPI!

## Authentication
### Open Token
The token returned from the SwitchBot Cloud is an encrypted open token that grants the user developer-level permissions. The user will be able to add, delete, edit, and look up his or her user data including profile data and data associated with the devices that have been added to the user's account.

## Glossary

The following table provides definitions to the terms to be frequently mentioned in the subsequent sections.

| Term          | Description                                                  |
| ------------- | ------------------------------------------------------------ |
| Hub           | Generally referred to these devices, SwitchBot Hub Model No. SwitchBot Hub S1/SwitchBot Hub Mini Model No. W0202200/SwitchBot Hub Plus Model No. SwitchBot Hub S1 |
| Hub Mini      | Short for SwitchBot Hub Mini Model No. W0202200              |
| Hub Plus      | Short for SwitchBot Hub Plus Model No. SwitchBot Hub S1      |
| Bot           | Short for SwitchBot Bot Model No. SwitchBot S1               |
| Curtain       | Short for SwitchBot Curtain Model No. W0701600               |
| Plug          | Short for SwitchBot Plug Model No. SP11                      |
| Meter         | Short for SwitchBot Thermometer and Hygrometer Model No. SwitchBot MeterTH S1 |
| Smart Fan     | Short for SwitchBot Smart Fan Model No. W0601100             |
| Cloud Service | An SwitchBot app feature that 1. enables SwitchBot products to be discovered and communicated with third-party services voice control services, 2. allows users to create customized smart scenes and Android widgets. For BLE-based devices such as Bot and Curtain, you MUST first add a Hub/Hub Mini/Hub Plus and then enable Cloud Service on the Settings page in order to make use of the web API! |

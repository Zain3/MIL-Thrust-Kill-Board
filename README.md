# MIL-Thrust-Kill-Board
**Description**: This board receives CAN messages from NaviGator's on-board computer to 1) Control thrust to the T200 thrusters on-board, and 2) If it doesn't receive a periodic heartbeat from the computer, it'll also shut off the thrusters, klling the sub.

**Longer Description**: The Purpose of this board is to receive CAN messages computer on-board NaviGator, where software wants to send thrust commands to the T200 Thrusters on-board.
This "Thrust Kill Board" can thus control ESC's connected to the thrusters to control thrust, or a HES can be pressed, which can manually turn on and off the thrusters to the submarine, shutting them down.
Finally, this board expects a "heartbeat" CAN message from the computer- if it doesn't receive it on time, it'll cut power to the thrusters, by turning off a relay.

# Firmware:
* How this Code Works:
* Purpose: To take in signals from the main computer via CAN, to modify the PWM
        and relay control of the on-board thrusters.

* The struct, "MIL_CAN_MailBox_t", encodes every CAN message

This board receives 2 types of CAN messages...
1. One struct to receive heart-beat from Computer
2. One struct to receive Thrust Messages from Computer

It also Kills or Unkills the Sub if it detects the HE sensor on the PCB is pressed

1. If it doesn't receive a heart-beat from the computer on time, it'll Kill the Sub by turning off all the Realys
2. Every time it receives Thrust Messages, it'll modify the PWM of the ESC's, using the written Blue Robotics Basic ESC Drivers to control the T200 Thrusters.

KillSub():
    - Sets PWM of thrusters to 0
    - Stops sending current to the Relay, cutting off power to the Thrusters


# PCB
* The PCB shows the 1) MCU, HE Sensor, Power, etc., and 2) The Relays, Power, and Switches Module
* The MCU can turn on and off all of the relays at once, which are each connected to a NPN Transistor Relay Switch Circuit.


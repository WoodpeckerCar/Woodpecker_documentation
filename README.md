![repo image](img/woodpecker.png)
#Woodpecker open source electric vehicle platform with negative carbon footprint.
https://woodpeck.org/ 
##Design documentation and Operating Manual of Drive by wire systems

#Operation
There are following operating modes: manual, wireless, remote and autonomous. 
All mechanical actuators - steering, brakes and accelerator are managed by electronic controllers / signals.

- **Manual mode** Manual mode is ordinary, stock Woodpecker driving mode by wired USB joystick. 
- **Wireless**    Wireless mode is done by radio controller (like Taranis X9D Plus) in vehicle VLOS - visual line of sight.
- **Remote**      Vehicle operation in BVLOS - Beyond Visual Line of Sight- mode by remote operator through Internet connection.
- **Autonomous**  Vehicle operated by on board autonomous driving system.

#Manual mode
##Switching ON Manual mode

1. Switch Power ON switch (power up brake and EPAS )on front panel. Red signal light must light on. 
2. Make sure "Remote control override" switch is ON (disable need for radio controller signal)
3. Switch on "Lights ON" switch on front panel (power up all CAN controllers and Joystick micro computer.
4. Turn key - "Ignition ON 72V" - Switch on 72V contactor for motor contollers[Make sure all 5 mushroom Emergency STOP are released]
5. Wait for 30-50 sec to boot up Joystick micro computer. Joystick demo application should startup automatically.
6. Press START on joystick controller [Should hear clicking noise of controller relays] to enable controller.
7. Press Y to switch on ignition. Wait for 2-3 sec.switch on Motor controllers;
8. Use joystick controls to drive, steer, brake, accelerate and switch between FRW and REV.

##Emergency stop.
- Active (electrical power available for dbw systems) vs Passive (total power failure) 
[Future feature]PASSIVE emergency stop (spring based motor clutch) which is engaged automatically, in case of total power loss.

PASSIVE Emergency stop 
1. Push any of 5 Emergency mushroom switches to disable motors
2. Press brake on joystick controller

- Vehicle is static vs Vehicle is moving
Use PASSIVE Emergency stop in both cases, ACTIVE (if implemented) if vehicle is moving.

1. Operator is in the vehicle or next to it.
2. Operator is not in vehicle, but in VLOS - visual line of sight

##Switching OFF Manual mode

1. Press X to turn ignition OFF.
2. Press BACK to disable controls
3. Switch off "Ignition OFF 72V" on front panel.

#Wireless mode
##Switching ON Wireless mode

1. Switch Power ON switch (power up brake and EPAS )on front panel. Red signal light must light on. 
2. Make sure "Remote control override" switch is OFF (disable need for radio controller signal)
3. Switch on "Lights ON" switch on front panel (power up all CAN controllers and Joystick micro computer.
4. Turn ON Radio transmitter and wait for connection to remote reciever
5. Turn "Ignition ON 72V" by SF switch on remote
6. Turn motor controllers on by SA switch.
7. Turn on DBW controllers in armed state by SE switch
8. Use joystick controls to drive, steer, brake, accelerate and switch between FRW and REV (SG switch).

##Emergency stop.

PASSIVE Emergency stop 
1. Push any of 5 Emergency mushroom switches to disable motors
2. Switch OFF radio transmitter - all controls should switch to OFF state

- Vehicle is static vs Vehicle is moving
Use PASSIVE Emergency stop in both cases, ACTIVE (if implemented) if vehicle is moving.

##Switching OFF Wireless mode

1. Switch all switches on OOFF state on remote or switch Remote OFF.
3. Switch off "Ignition OFF 72V" on front panel and "Lights OFF" switches.


#Remote mode
##Switching ON Remote mode

1. Switch Power ON switch (power up brake and EPAS )on front panel. Red signal light must light on. 
2. Make sure "Remote control override" switch is ON (disable need for radio controller signal)
3. Switch on "Lights ON" switch on front panel (power up all CAN controllers and Joystick micro computer (REMOTE CONTROL GATEWAY).
4. Use REMOTE CONTROL GATEWAY UDP-CAN conversion controls to drive, steer, brake, accelerate and switch between FRW and REV (SG switch).

##Emergency stop.

PASSIVE Emergency stop 
1. Push any of 5 Emergency mushroom switches to disable motors
2. Remotely Switch OFF REMOTE CONTROL GATEWAY - all controls should switch to OFF state

- Vehicle is static vs Vehicle is moving
Use PASSIVE Emergency stop in both cases, ACTIVE (if implemented) if vehicle is moving.

On vehicle Operator -
OFF vehicle Operator -

##Switching OFF Remote mode

1. Remotely switch OFF REMOTE CONTROL GATEWAY.
3. Switch off "Ignition OFF 72V" on front panel and "Lights OFF" switches.


##Mode Overrides 

### From manual to remote
TBD

### From remote to manual
TBD

#Main DbW components.

Drive By Wire system consists from:

**1. Accelerator Controller**

Connected to motor controllers. Receive commands and provide report via DbW CAN messages. 

**2. Brake Controller.**

Connected to hydraulic brake unit. Receive commands and provide report via DbW CAN messages.

**3. PWM CAN Gateway.**

Connected to CAN, 4 relay block and radio remote. 

**4. CAN Gateway**

Bridge between controller CAN and DbW CAN to transmit RPM,Vehicle Speed, current and Voltage  messages.

**5. Joystick micro computer**

Raspberry Pi micro computer Logitech F310 gamepad attached via USB port. Connected to DbW CAN. 
Bash script for automatic joystick launch is located @ /home/pi/dbwstart.sh
Script is being launched on bootup from config file /etc/rc.local

content of .dbstart.sh script:
```
#!/bin/bash

sudo ip link set can0 type can bitrate 500000
sudo ip link set up can0
sudo ip link set can1 type can bitrate 500000
sudo ip link set up can1
cd /home/pi/XXXX/build
./oscc-joystick-commander 0
```

Access information:
```
Connect using SSH to XXXXXXXX:22
User: XXX
Password: XXX
```

#CAN buses
There are 2 CAN buses on vehicle. Both are connected with CAN Gateway module. DbW CAN screw terminal is located in side of the glow box compartment.

1. DbW CAN bus. - 500k

Connected devices: CAN GW, Brake controller, Accelerator controller, Control Processor, CAN Gateway, 

2. Motor controller CAN - 250k

Connected devices: Motor Controllers , CAN GW

#Controls


##Joystick operation

```
START - Enable controls
BACK - Disable controls
LEFT TRIGGER - Brake
RIGHT TRIGGER - Throttle
LEFT STICK - Steering
Y - Ignition ON
X - Ignition OFF
B - Starter ON
```







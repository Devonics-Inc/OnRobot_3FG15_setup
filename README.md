# OnRobot 3FG15 ->Fairino setup
This repo contains a README with steps to set up controls for your OnRobot 3 Finger Gripper (3FG) for either IO or Modbus RTU communication.

#### Step 0 will be the same for both modbus and IO communication

### Step 0: Connecting your gripper and the OnRobot Quick Changer
#### Connect your gripper to the mounting plate by sliding the metal bar into the latch of the plate (shown below):

![alt text](image-1.png)

# Setting up the OnRobot gripper for IO communication:
#### IO communication will limit you to 256 IO combinations that can have control for gripper force, target diameter, etc.

    Find the m8 to m12 connection cable in the OnRobot box. Connect this wire to the quick changer as shown here (wire bracket optional):

![alt text](image.png)



    Connect the other end of the data cable to the OnRobot control box using the m12 port on the front (shown below):

![alt text](image-2.png)


    Finally, use a kettle lead and the provided 24v adapter to the OnRobot control box (shown below):

![alt text](image-3.png)

### Step 1: Wiring of the Fairino control box and OnRobot control box
     First, you'll want to take your external power supply and connect the positive to the E-24v port on the top rail and the ground to any E-0v port on the Fairino control box

     Find and insert the green screw terminal block for the back of the OnRobot box.

     After inserting the screw terminal block, use one of the provided wires to connect the GND pin of the OnRobot control box to another E-0v pin on the Fairino control box.

     Finally, grab the other green screw terminal for the DI block of the OnRobot Control box. This is what will give your griper IO communication with your Fairino Control Box

#### Your wiring set up should look like this:

    OnRobot Control Box
        L screw terminal block
        |    L GND->Fairino:E-0v
        |
        L Device cable -> OnRobot gripper bracket
        |
        L 24V port -> kettle lead -> wall outlet
        |
        L DI screw terminal
            L DIx <-> Fairino:DOx

    Fairino Control Box
        L IO Terminal Block
        |    L E-24V -> Power supply (+)
        |    L E-0V -> Power supply (-)
        L DOx <-> OnRobot:DIx

### Step 2: Creating your gripper program
    Connect your ethernet cable from your OnRobot control box to your computer.

    In any browser, type in the IP address of your OnRobot control box (default 192.168.1.1) to navigate to the WebClient.

    Navigate to *"WebLogic"* -> *"Program Editor"*
![alt text](image-4.png)

    Here, you can create programs that will control your gripper. You can only have one program running on your gripper at a time, but this program can contain all of your IO mappings that your gripper will response to.

    To select a main program for your gripper to run on start up, just select and run your custom program until you turn off your control box. When power is lost to the control box, it will restart the previously running program when it turns back on.


# Setting up your gripper for Modbus RTU communication
#### This method of modbus communication will be controlled by the lua programs in the Fairino web app. Before using the modbus control, please note the disclaimed below. 

#### Disclaimer:
![alt text](<Screenshot from 2025-08-05 14-42-16.png>)

### Step 1: Connecting your gripper via Modbus RTU 
    Find the m12-8pin cable with exposed wires on the end (7 wires: 3 24v, 3 GND, 1 PE)

    Connect ONE of the 24V and GND to your 24V 1.5A power supply 

    Connect the RS485 pins to the appropriate ports in the pin block of the Fairino control box

    Now, you can connect the m8-8pin to m12-8pin. This will plug into your gripper and allow modbus communication from the control box to the gripper.


### Step 2: Programming your gripper through the Fairino web app:
    To set up your robot for modbus communication, you need to open the Fairino web app by opening any web browser and entering the IP address of your control box into the url (default IP is 192.168.58.2)

    If it is your first time powering on the control box, it will ask you to enter the serial number (located on a small, silver sticker on top of the control box) then power cycle.
    
    Log in using username "admin" and password "123"

    Navigate to Application->Tool App -> Peripheral Protocol and where it says "Extention Axis" in the drop down, select "Modbus Master" (shown below)

![alt text](<Screenshot from 2025-08-06 11-02-47.png>)


### Step 3: Programming your gripper in the Web App

    Use the Lua progamming guide provided in this repo to use modbus read and write commands in your program. For register mapping and other information, reference the attached images below:

    Developer Note: Setting the "target diameter" or other "target" paramters will not cause your gripper to move. After setting the "target" registers, you must call the "grip" function with the "Control" register (addr 0x03).


![alt text](<Screenshot from 2025-08-05 14-41-31.png>)

![alt text](<Screenshot from 2025-08-05 14-41-48.png>)

![alt text](<Screenshot from 2025-08-05 14-42-01.png>)

*Thank you to OnRobot for providing images from the User Manual*
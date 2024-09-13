# Week 5 - Multitask

Let's run how we can make our robot do multiple things at the same time!

## `pybricks.tools.multitask`

!!! note

    Reference: **Pybricks Documentations**

    - [Pybricks Modules - tools](https://docs.pybricks.com/en/latest/tools/index.html) 
        -  [Multitaskinig](https://docs.pybricks.com/en/latest/tools/index.html?multitasking#multitasking)

### Example


| Port | Function | Note |
| ---- | -------- | ---- |
| Port `A` | Drive Base - Left Motor | |
| Port `E` | Drive Base - Right Motor | |
| Port `D` | Forklift Motor | Clockwise rotation to lift up |


=== "`forklift.py`"

    ```python
    from pybricks.hubs import InventorHub
    from pybricks.pupdevices import Motor, ColorSensor, UltrasonicSensor, ForceSensor
    from pybricks.parameters import Button, Color, Direction, Port, Side, Stop, Axis
    from pybricks.robotics import DriveBase
    from pybricks.tools import wait, StopWatch
    from pybricks.tools import multitask, run_task
    import constants

    hub = InventorHub(top_side=Axis.Z)

    lift = Motor(Port.D)

    wheel_e = Motor(Port.E, reset_angle=True)
    wheel_a = Motor(Port.A, Direction.COUNTERCLOCKWISE, reset_angle=True)

    drive_base = DriveBase(left_motor=wheel_a, 
        right_motor=wheel_e, 
        wheel_diameter=constants.WHEEL_DIAMETER,
        axle_track=constants.AXLE_LENGTH)

    SPEED = 120

    drive_base.settings(straight_speed=SPEED,
        straight_acceleration=300, 
        turn_rate=SPEED, 
        turn_acceleration=300)

    drive_base.use_gyro(use_gyro=True)

    # Compensate lift horizontal offset
    async def drive_back_and_up():
        await drive_base.straight(-50)
        await drive_base.straight(50)

    # Move forklift up and down while adjusting the robot position to compensate offset
    async def move_forklift_up_and_down():
        # await drive_base.straight(250)
        await multitask(drive_base.straight(-50), lift.run_angle(SPEED, 70))
        await multitask(drive_base.straight(50),  lift.run_angle(SPEED, 70))
        
        await multitask(drive_back_and_up(), lift.run_angle(SPEED, -140))
        # await drive_base.straight(-250)

    # Runs the main program from start to finish.

    drive_base.settings(straight_speed=900) # Make robot move faster
    drive_base.straight(300)

    drive_base.settings(straight_speed=SPEED) # Set drivebase to low speed
    run_task(move_forklift_up_and_down())

    drive_base.settings(straight_speed=900) # Make robot move faster again
    drive_base.straight(-300)
    ```

=== "`constants.py`"

    ```python
    #Dimensions of the robot in mm
    AXLE_LENGTH = 111
    WHEEL_DIAMETER = 55
    ```

!!! tip "Troubleshooting"

    ## Troubleshooging

    ### `NameError: name 'run_task' isn't defined`
        
    Did you import `run_task` module?

    ```python
    from pybricks.tools import multitask, run_task
    ```
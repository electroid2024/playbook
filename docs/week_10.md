# Auto-advancing Hub Menu

=== "`main.py`"

    ```python
    from pybricks.tools import hub_menu
    from pybricks.hubs import PrimeHub
    import constants

    # Initialize the hub.
    hub = PrimeHub()

    last_program = hub.system.storage(offset=constants.OFFSET_LAST_PROGRAM, read=1)
    if last_program == '1':
        selected = hub_menu("2", "3", "4", "5", "6", "7", "8", "9", "A", "B", "1", )
    elif last_program == '2':
        selected = hub_menu("3", "4", "5", "6", "7", "8", "9", "A", "B", "1", "2", )
    elif last_program == '3':
        selected = hub_menu("4", "5", "6", "7", "8", "9", "A", "B", "1", "2", "3", )
    elif last_program == '4':
        selected = hub_menu("5", "6", "7", "8", "9", "A", "B", "1", "2", "3", "4", )
    elif last_program == '5':
        selected = hub_menu("6", "7", "8", "9", "A", "B", "1", "2", "3", "4", "5", )
    elif last_program == '6':
        selected = hub_menu("7", "8", "9", "A", "B", "1", "2", "3", "4", "5", "6", )
    elif last_program == '7':
        selected = hub_menu("8", "9", "A", "B", "1", "2", "3", "4", "5", "6", "7", )
    elif last_program == '8':
        selected = hub_menu("9", "A", "B", "1", "2", "3", "4", "5", "6", "7", "8", )
    elif last_program == '9':
        selected = hub_menu("A", "B", "1", "2", "3", "4", "5", "6", "7", "8", "9", )
    elif last_program == 'A':
        selected = hub_menu("B", "1", "2", "3", "4", "5", "6", "7", "8", "9", "A", )
    elif last_program == 'B':
        selected = hub_menu("1", "2", "3", "4", "5", "6", "7", "8", "9", "A", "B", )
    else:
        print(f"[Warning] unknown last_program: {last_program}")
        selected = hub_menu("1", "2", "3", "4", "5", "6", "7", "8", "9", "A", "B", )

    if selected == "1":
        import mission_1
    elif selected == "2":
        import mission_2
    elif selected == "3":
        import mission_3
    elif selected == "4":
        import mission_4
    elif selected == "5":
        import mission_5
    elif selected == "6":
        import mission_6
    elif selected == "7":
        import mission_7
    elif selected == "8":
        import mission_8
    elif selected == "9":
        import mission_9
    elif selected == "A":
        import mission_a
    elif selected == "B":
        import mission_b

    ```

=== "`mission_1.py`"

    ```python
    from pybricks.hubs import InventorHub
    from pybricks.pupdevices import Motor, ColorSensor, UltrasonicSensor
    from pybricks.parameters import Button, Color, Direction, Port, Side, Stop, Axis
    from pybricks.robotics import DriveBase
    import constants

    hub = InventorHub(top_side=Axis.Z)

    motor_l = Motor(Port.A, reset_angle=True)
    motor_r = Motor(Port.B, Direction.COUNTERCLOCKWISE, reset_angle=True)

    drive = DriveBase(left_motor=motor_l, 
        right_motor=motor_r, 
        wheel_diameter=constants.WHEEL_DIAMETER,
        axle_track=constants.AXLE_LENGTH)

    drive.settings(straight_speed=920,
        straight_acceleration=900, 
        turn_rate=920, 
        turn_acceleration=900)
    drive.use_gyro(use_gyro=True)

    drive.straight(distance=100)

    # Save the last-ran program
    hub.system.storage(offset=constants.OFFSET_LAST_PROGRAM, write="1")
    ```

=== "`mission_2.py`"

    ```python
    from pybricks.hubs import InventorHub
    from pybricks.pupdevices import Motor, ColorSensor, UltrasonicSensor
    from pybricks.parameters import Button, Color, Direction, Port, Side, Stop, Axis
    from pybricks.robotics import DriveBase
    import constants

    hub = InventorHub(top_side=Axis.Z)

    motor_l = Motor(Port.A, reset_angle=True)
    motor_r = Motor(Port.B, Direction.COUNTERCLOCKWISE, reset_angle=True)

    drive = DriveBase(left_motor=motor_l, 
        right_motor=motor_r, 
        wheel_diameter=constants.WHEEL_DIAMETER,
        axle_track=constants.AXLE_LENGTH)

    drive.settings(straight_speed=920,
        straight_acceleration=900, 
        turn_rate=920, 
        turn_acceleration=900)
    drive.use_gyro(use_gyro=True)

    drive.straight(distance=200)

    # Save the last-ran program
    hub.system.storage(offset=constants.OFFSET_LAST_PROGRAM, write="2")
    ```

=== "`constants.py`"

    ```python
    #Dimensions of the robot in mm
    AXLE_LENGTH = 111
    WHEEL_DIAMETER = 54

    # System storage slot offset for storing last-ran program number
    OFFSET_LAST_PROGRAM = 10
    ```
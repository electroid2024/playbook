# Auto-advancing Hub Menu

=== "`main.py`"

    ```python
    from pybricks.tools import hub_menu
    from pybricks.hubs import InventorHub
    import constants

    import mission_1, mission_2, mission_3, mission_4, mission_5, mission_6, mission_7, mission_8, mission_9, mission_a, mission_b

    # Initialize the hub.
    hub = InventorHub()

    while True:
        last_program = hub.system.storage(offset=constants.OFFSET_LAST_PROGRAM, read=1)
        if last_program == b'1':
            selected = hub_menu("2", "3", "4", "5", "6", "7", "8", "9", "A", "B", "1", )
        elif last_program == b'2':
            selected = hub_menu("3", "4", "5", "6", "7", "8", "9", "A", "B", "1", "2", )
        elif last_program == b'3':
            selected = hub_menu("4", "5", "6", "7", "8", "9", "A", "B", "1", "2", "3", )
        elif last_program == b'4':
            selected = hub_menu("5", "6", "7", "8", "9", "A", "B", "1", "2", "3", "4", )
        elif last_program == b'5':
            selected = hub_menu("6", "7", "8", "9", "A", "B", "1", "2", "3", "4", "5", )
        elif last_program == b'6':
            selected = hub_menu("7", "8", "9", "A", "B", "1", "2", "3", "4", "5", "6", )
        elif last_program == b'7':
            selected = hub_menu("8", "9", "A", "B", "1", "2", "3", "4", "5", "6", "7", )
        elif last_program == b'8':
            selected = hub_menu("9", "A", "B", "1", "2", "3", "4", "5", "6", "7", "8", )
        elif last_program == b'9':
            selected = hub_menu("A", "B", "1", "2", "3", "4", "5", "6", "7", "8", "9", )
        elif last_program == b'A':
            selected = hub_menu("B", "1", "2", "3", "4", "5", "6", "7", "8", "9", "A", )
        elif last_program == b'B':
            selected = hub_menu("1", "2", "3", "4", "5", "6", "7", "8", "9", "A", "B", )
        else:
            print(f"[Warning] unknown last_program: {last_program}")
            selected = hub_menu("1", "2", "3", "4", "5", "6", "7", "8", "9", "A", "B", )

        if selected == "1":
            mission_1.run()
        elif selected == "2":
            mission_2.run()
        elif selected == "3":
            mission_3.run()
        elif selected == "4":
            mission_4.run()
        elif selected == "5":
            mission_5.run()
        elif selected == "6":
            mission_6.run()
        elif selected == "7":
            mission_7.run()
        elif selected == "8":
            mission_8.run()
        elif selected == "9":
            mission_9.run()
        elif selected == "A":
            mission_a.run()
        elif selected == "B":
            mission_b.run()
    ```

=== "`mission_1.py`"

    ```python
    from pybricks.hubs import InventorHub
    from pybricks.pupdevices import Motor, ColorSensor, UltrasonicSensor
    from pybricks.parameters import Button, Color, Direction, Port, Side, Stop, Axis
    from pybricks.robotics import DriveBase
    import constants

    def run():
            
        hub = InventorHub(top_side=Axis.Z)

        motor_l = Motor(Port.A, Direction.COUNTERCLOCKWISE, reset_angle=True)
        motor_r = Motor(Port.B, reset_angle=True)

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

        motor_l.close()
        motor_r.close()

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

    def run():

        hub = InventorHub(top_side=Axis.Z)

        motor_l = Motor(Port.A, Direction.COUNTERCLOCKWISE, reset_angle=True)
        motor_r = Motor(Port.B, reset_angle=True)

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

        motor_l.close()
        motor_r.close()

        # Save the last-ran program
        hub.system.storage(offset=constants.OFFSET_LAST_PROGRAM, write="2")

    ```

=== "`constants.py`"

    ```python
    #Dimensions of the robot in mm
    AXLE_LENGTH = 111
    WHEEL_DIAMETER = 87

    # System storage slot offset for storing last-ran program number
    OFFSET_LAST_PROGRAM = 10
    ```
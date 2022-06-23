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
def mean_camber_line_yc(m, p, X):
    """ mean camber line y-coordinates from x = 0 to x = p
    m: maximum camber in percentage of the chord
    p: position of the maximum camber in tenths of chord
    """
    return np.array([
        (m / np.power(p, 2)) * ((2 * p * x) - np.power(x, 2)) if x < p
        else (m / np.power(1 - p, 2)) * (1 - (2 * p) + (2 * p * x) - np.power(x, 2)) for x in X
    ])
def thickness_distribution(t, x):
    """ Calculate the thickness distribution above (+) and below (-) the mean camber line
    t: airfoil thickness
    x: coordinates along the length of the airfoil, from 0 to c
    return: yt thickness distribution
    """
    coeff = t / 0.2
    x1 = 0.2969 * np.sqrt(x)
    x2 = - 0.1260 * x
    x3 = - 0.3516 * np.power(x, 2)
    x4 = + 0.2843 * np.power(x, 3)
    # - 0.1015 coefficient for open trailing edge
    # - 0.1036 coefficient for closed trailing edge
    x5 = - 0.1036 * np.power(x, 4)
    return coeff * (x1 + x2 + x3 + x4 + x5)
def dyc_dx(m, p, X):
    """ derivative of mean camber line with respect to x
    m: maximum camber in percentage of the chord
    p: position of the maximum camber in tenths of chord
    """
    return np.array([
        (2 * m / np.power(p, 2)) * (p - x) if x < p
        else (2 * m / np.power(1 - p, 2)) * (p - x) for x in X
    ])
# ==============================================================
# final coordinates for the airfoil upper and lower surface

def x_upper_coordinates(x, yt, theta):
    """ final x coordinates for the airfoil upper surface """
    return x - yt * np.sin(theta)


def y_upper_coordinates(yc, yt, theta):
    """ final y coordinates for the airfoil upper surface """
    return yc + yt * np.cos(theta)


def x_lower_coordinates(x, yt, theta):
    """ final x coordinates for the airfoil lower surface """
    return x + yt * np.sin(theta)


def y_lower_coordinates(yc, yt, theta):
    """ final y coordinates for the airfoil lower surface """
    return yc - yt * np.cos(theta)


def theta(dyc, dx):
    return np.arctan(dyc / dx)

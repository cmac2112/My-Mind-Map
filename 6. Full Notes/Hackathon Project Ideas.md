

# Rework of EZDocuments
EZDocuments was my project for the hackathon at KU. This project generated a lot of interest but lacked a proper UI (why it didnt win). There are still people out there wanting me to make this into a full project one day. 

I believe we should steal code (usually legal) from this during a hackathon to get us going and rework this project. If we can get this right it can compete for top 3

1. EZdocuments allows users to log in through their google accounts through Google Oauth. The program then grabs all of the user's google document's that contain 'notes' in the title. 
2. It then sends all notes as context to a LLM (Google Gemini) to allow users to ask questions about their notes. 
3. Users can do more than just ask questions about their notes, they can also make the LLM generate practice tests based off of their notes, which is completely unique and no other LLM/GPT site that i have seen does this.

What would need reworked
- api keys are probably expired 
- code is outdated for the rapidly changing GPT/LLM landscape
- I dont even know what the frontend looks like anymore or how it works because it was built with GPT
New name - Note buddy, or something


# Nasa spaceapps challenge notes

keplarian elements
1. **Semi-major axis (a)**: Defines the size of the conic.
2. **Eccentricity (e)**: Defines the shape of the conic.
3. **Inclination (i)**: The angle between the reference frame and the orbital plane.
4. **Longitude of the ascending node (Ω)**: The pin.
5. **Argument of periapsis (ω)**: The twist.
6. **Mean anomaly at epoch (v)**: The angle.

![[Pasted image 20240927182827.png]]
Semi major axis - 
size - length of half of the major axis (also known as the semi-major axis)
(a)
Eccentricty: 
if you were to move the minor axis this would change the eccentricity, 
e
directly related to the radius of the periapsis and the radius of the apoapsis, and depends on the major axis (a)
Inclination:
Tilt of the orbit measured in degrees from the orbital plane and the equatorial plane

Longitude of Acending Node: (omega) measured in degrees,
along the equitorial plane along the vernal equinox to the acending node

Location of the periapsis: argument of periapsis
(omega) measured in degrees, line of acending node to the periapsis along the orbital plane


### Orbital Elements

- Semi-major axis, `a = 1.52371034`
- Eccentricity, `e = 0.09339410`
- Inclination, `I = 50.84969142°`
- Mean longitude, `L = -4.55343205°`
- Longitude of perihelion, `longPeri = -23.94362959°`
- Longitude of ascending node, `longNode = 49.55953891°`
- Given time, `time = 1727473.172396`

### Step 1: Orbital Period

We calculate the orbital period using Kepler's Third Law:

![[Pasted image 20240928134906.png]]
### Step 2: Adjusted Time

Adjusted time `T_adj` is:

![[Pasted image 20240928134928.png]]
### Step 3: Mean Anomaly (M)

Now, calculate the mean anomaly `M`:

![[Pasted image 20240928134956.png]]

### Step 4: Eccentric Anomaly (E)

We start with E=M=348.33°E = M = 348.33°E=M=348.33°, and iterate using:

![[Pasted image 20240928135021.png]]
Repeating this iteration 4 more times gives us an approximate solution:

E≈347.49°E \approx 347.49°E≈347.49°

### Step 5: True Anomaly (v)

Now calculate the true anomaly `v` using:

![[Pasted image 20240928135046.png]]

### Step 6: Distance (r)

![[Pasted image 20240928135058.png]]
### Step 7: Orbital Plane Coordinates

We calculate the heliocentric coordinates in the orbital plane:

![[Pasted image 20240928135119.png]]
### Step 8: Convert to 3D Coordinates


-![[Pasted image 20240928135146.png]]
### Final 3D Position:

The position of the body at time `1727473.172396` is approximately:

![[Pasted image 20240928135231.png]]

This gives us the heliocentric coordinates of the body in 3D space!


### 1. **Orbit of the Moon (Relative to the Planet):**

To compute the moon's position, you would need its orbital elements relative to the planet. These elements are similar to the planet’s orbital elements around the star, but instead of referencing the star, they reference the planet as the central body.

Key parameters would include:

- **Semi-major axis (`a_moon`)**: Distance between the moon and the planet.
- **Eccentricity (`e_moon`)**: Shape of the moon's orbit.
- **Inclination (`I_moon`)**: Tilt of the moon's orbit relative to the planet’s equatorial plane.
- **Mean longitude (`L_moon`)**: The moon's mean longitude.
- **Longitude of perihelion (`longPeri_moon`)**: Position of the periapsis of the moon's orbit relative to the planet.
- **Longitude of ascending node (`longNode_moon`)**: Position of the ascending node of the moon's orbit relative to the planet.

Once you have these elements, you can calculate the moon’s position relative to the planet using the same orbital mechanics described previously (using the `calculatePosition` function adapted for the moon).

### 2. **Calculate Moon's Position Relative to the Planet:**

Using the moon’s orbital elements relative to the planet, you would:

1. **Calculate the moon’s position in its orbit relative to the planet’s center** using the same process: solving for the mean anomaly, eccentric anomaly, true anomaly, distance, and 2D orbital plane coordinates.
2. **Convert these to 3D coordinates** by accounting for the moon’s orbital inclination and ascending node (relative to the planet).

This gives you the moon’s position in the planet-centered frame of reference.

### 3. **Combine Positions (Planet and Moon):**

Now, to get the moon's heliocentric position (relative to the star), you simply combine the planet's heliocentric position with the moon’s position relative to the planet. This works as follows:

- Let **(xplanet,yplanet,zplanet)(x_{planet}, y_{planet}, z_{planet})(xplanet​,yplanet​,zplanet​)** be the heliocentric coordinates of the planet (calculated earlier).
- Let **(xmoon/planet,ymoon/planet,zmoon/planet)(x_{moon/planet}, y_{moon/planet}, z_{moon/planet})(xmoon/planet​,ymoon/planet​,zmoon/planet​)** be the geocentric (planet-centered) coordinates of the moon (from the moon's orbit calculation).

Then the moon's heliocentric coordinates are:

![[Pasted image 20240928135736.png]]
This gives you the moon’s position relative to the central star.

### Example:

Let’s assume the moon’s orbit has the following orbital elements relative to the planet:

- **Semi-major axis**: amoon=0.00257 AUa_{moon} = 0.00257 \text{ AU}amoon​=0.00257 AU (typical for a moon like our own).
- **Eccentricity**: emoon=0.0549e_{moon} = 0.0549emoon​=0.0549.
- **Inclination**: Imoon=5.145°I_{moon} = 5.145°Imoon​=5.145°.
- **Mean longitude**: Lmoon=0°L_{moon} = 0°Lmoon​=0° (arbitrary starting point).
- **Longitude of perihelion**: longPerimoon=0°longPeri_{moon} = 0°longPerimoon​=0°.
- **Longitude of ascending node**: longNodemoon=0°longNode_{moon} = 0°longNodemoon​=0°.

Now we calculate the moon's position in the planet’s orbit:

- Using the same procedure, we solve for the moon's position relative to the planet.

Let’s say the result is:

![[Pasted image 20240928135809.png]]


# shaders
https://www.youtube.com/watch?v=vM8M4QloVL0



Landing page
information page - about Keplerian parameters\
Simulation page - simulation page


clickable planets - zoom in on them show data


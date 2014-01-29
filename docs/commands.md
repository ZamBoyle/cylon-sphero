# Commands

## abortMacro → (ID code , command number)

Public: This command aborts any executing macro, and returns both it's ID code
and the command number currently in progress.

Returns an array containing the ID code and command number.

## abortOrbBasicProgram

Public: Aborts execution of any currently-running orbBasic program.

Returns null.

## appendMacroChunck(chunk)

Public: Stores an attached macro definition into a temporary RAM buffer for
later execution. It's similar to the `saveTemporaryMacro` function, but allows
you to build up a longer temporary macros.

- **chunk** - macro definition to be executed later. Will throw an
  error if any larger than 254 bytes.

Returns a boolean indicating whether or not the macro could be packeted.

## appendOrbBasicFragment(area, programCode)

Public: Appends a fragment of an orbBasic program to a buffer that will be
written to the Sphero eventually.

- **area** - value to start buffer with
- **fragment** - fragment of orbBasic to be sent to the Sphero. Will throw an
  error if larger than 253 bytes

Returns a boolean indicating whether or not the fragment could be packeted

## configureCollisionDetection(method, thresholdX, thresholdY, speedX, speedY, deadTime)

Internal: Configures collision detection on the Sphero, using the provided
params to decide what constitutes a 'collision'.

- **method** - detection method to use. Pass `0x01` to enable collision detection
- **thresholdX** - an 8-bit settable threshold for the X axis of the Sphero.
  A setting of `0x00` disables the contribution of this axis
- **thresholdY** - an 8-bit settable threshold for the Y axis of the Sphero.
  A setting of `0x00` disables the contribution of this aYis
- **speedX** - an 8-bit settable speed value for the X speed. This is ranged,
  then added to `thresholdX` to generate the final threshold value.
- **speedY** - an 8-bit settable speed value for the Y speed. This is ranged,
  then added to `thresholdY` to generate the final threshold value.
- **deadTime** - an 8-bit post-collision dead time to prevent re-triggering of
  the collision event. Specified in 10ms increments

Returns a boolean whether or not the packet to be sent to the Sphero has been
built successfully

## configureLocator(flag, x, y, yawTare)

Public: Through the streaming interface, Sphero provides real-time location
data in the form of X, Y coordinates on the ground plane.

  - **flag** - number (0-1), determines whether the calibrate commands automatically set the
    yaw tare value.
  - **y** - set the current X coordinates of Sphero on the ground plane in
    centimeters.
  - **x** - set the current Y coordinates of Sphero on the ground plane in
    centimeters.
  - **yawTare** - (0-359) value for the orientation the Sphero should use after
    calibration.

Returns a boolean whether or not the packet to be sent to the Sphero has been
built successfully

## detectCollisions

Public: Enables collision detection for the Sphero. When the Sphero detects
a collision, it will emit the `collision` event.

Shortcut method to `configureCollisionDetection` so you don't have to deal
with setting it up manually.

Returns nothing.

## eraseOrbBasicStorage(area)

Internal: This erases any existing program in the specified storage area.
Specify 00h for the temporary RAM buffer or 01h for the persistent storage area.

- **area** - which buffer should be erased, `0x00` for the temporary RAM buffer or
  `0x01` for the persistent storage area

Returns nothing.

## executeOrbBasicProgram(Area, Start Line, Start Line)

Public: This attempts to run a program in the specified storage area beginning
at the specified line number. This command will fail if there is already
an orbBasic program executing.

area - params

startLine - params

Returns null.

## getApplicationConfigurationBlock

Public: This allows you to retrieve the application configuration block that
is set aside for exclusive use by applications.

Returns null.

## getConfigurationBlock(ID)

Public: This command retrieves one of the configuration blocks.

id - params

Returns null.

## getDeviceMode → (Mode), options: 00h (Normal mode) | 01h (User Hack mode)

Public: Gets the operation mode of Sphero based on the supplied mode value.

Returns 00h (Normal mode) | 01h (User Hack mode).

## getMacroStatus → (ID code , cmd number, cmd number)

Public: This command returns the ID code and command number of the currently
executing macro.

Returns (ID code, cmd number, cmd number).

## getPermanentOptionFlags → (FLAGS), options: 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 6-31

Public: This command returns the ID code and command number of the currently
executing macro.

Returns an array of option flags

## getRGB → (red,green,blue) | (color)

Public: This retrieves the "user LED color" which is stored in the config
block.

Returns the sphero's LED color

## getTemporaryOptionFlags → (FLAGS), options: 0 | 1-31

Public: Returns the temporary option flags.

Returns FLAGS

## reInitializeMacroExecutive

Public: This terminates any running macro and reinitializes the macro system.

Returns null.

## readLocator → (XPOS, YPOS, XVEL, YVEL, SOG)

Public: This reads Sphero's current position (X,Y), component velocities and
SOG (speed over ground).

Returns (XPOS, YPOS, XVEL, YVEL, SOG).

## roll(speed, heading, state)

Public: This commands Sphero to roll along the provided vector. Both a speed
and a heading are required; the latter is considered relative to the last
calibrated direction.

speed - params
heading - params
state - params

Returns null.

## runMacro(SEQ, DLEN, ID)

Public: This attempts to execute the specified macro.

seq - params
dLen - params
id - params

Returns null.

## saveMacro(data)

Public: This stores the attached macro definition into the persistent store
for later execution.

data - params

Returns null.

## saveTemporaryMacro(data)

Public: This command controls the self level routine.

options - params
angleLimit - params
timeout - params
trueTime - params

Returns options: array [(0 | 1 | 2 |3 ), (0 | 1 to 90), (0 | 1 to 255), (0 | 1 to 255)].

## selfLevel(Options, Angle Limit, Timeout, True Time), options: ((0 | 1 | 2 |3 ), (0 | 1 to 90), (0 | 1 to 255), (0 | 1 to 255)

Public: This command controls the self level routine.

range - params

Returns integer opt: 0 | 1 | 2 | 3.

## setAccelerometerRange(Range Idx), options: 0 | 1 | 2 | 3

## setApplicationConfigurationBlock

## setBackLED(level)

Public: This allows you to control the brightness of the back LED. The value does
not persist across power cycles.

level - params

Returns null.

## setBoostWithTime(STATE)

Public: setBoostWithTime(state)

state - params

Returns null.

## setColor(color)

Public: Allows for convenient setting of the Sphero's color using a hex value
or a color name string

- **color** - hex number (`0xFF1500`) or string color name to set the Sphero
  to
- **persist** - boolean, whether or not the color should persist. Defaults to
  `true`

Returns null.

## setRandomColor

Public: Changes the Sphero to a random color.

- **persist** - boolean, whether or not the color should persist. Defaults to
  `true`

Returns null.

## setConfigurationBlock(value)

Public: This command accepts an exact copy of the configuration block and
loads it into the RAM copy of the configuration block.

value - params

Returns null.

## setDataStreaming(N, M, MASK, PCNT, MASK2)

Public: Sphero supports asynchronous data streaming of certain control system and sensor parameters.

n - params
m -params
mask - params
pcnt - params
mask2 - params

Returns null.

## setDeviceMode(MODE)

Public: Assigns the operation mode of Sphero based on the supplied mode value.

mode - params

Returns null.

## setHeading(HEADING)

Public: This allows the smartphone client to adjust the orientation of Sphero
by commanding a new reference heading in degrees, which ranges from 0 to 359.

heading - params

Returns null.

## setMacroParameter(Param, Val1, Val2)

Public: This command allows system globals that influence certain macro
commands to be selectively altered from outside of the macro system itself.

param - params
val1 - params
val2 - params

Returns null.

## setMotionTimeout(TIME)

Public: This sets the ultimate timeout for the last motion command to keep
Sphero from rolling away in the case of a crashed (or paused) client app.

time - params

Returns null.

## setPermanentOptionFlags(FLAGS)

Public: Assigns the permanent option flags to the provided value and writes them
immediately to the config block for persistence across power cycles.

flags - params

Returns null.

## setRGB(color, persist)

Public: Allows for convenient setting of the Sphero's color using a hex value
or a color name string

- **color** - hex number (`0xFF1500`) or to set the Sphero to
- **persist** - boolean, whether or not the color should persist. Defaults to
  `true`

Returns null.

## setRawMotorValues(L-MODE, L-POWER, R-MODE, R-POWER)

Public: This allows you to take over one or both of the motor output values,
instead of having the stabilization system control them.

lMode - params
lPower - params
rMode - params
rPower - params

Returns null.

## setRotationRate(RATE)

Public: Sets the rotation rate of the Sphero

rate - params

Returns nothing

## setStabalisation(bool)

Public: Sets whether the Sphero should have stabilization enabled

bool - whether or not the sphero should have stabilization

Returns nothing

## setTemporaryOptionFlags(FLAGS)

Public: Assigns the temporary option flags to the provided value. These do not
persist across a power cycle. See below for the bit definitions.

flags - params

Returns null.

## stop

Public: Stops the Sphero from rolling around.

Returns nothing

## submitValueToInputStatement(VAL)

Public: This takes the place of the typical user console in orbBasic and allows a
user to answer an input request.

val - params

Returns null.

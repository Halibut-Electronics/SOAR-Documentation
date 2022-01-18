# User's Guide
## User Interface
Indicators:
* Power LED: Lit if power is applied.
* GPS LED: Lit whenever the GPS send a PPS (Pulse Per Second) to the CPU. This is an indication that the GPS thinks it is sync'd.
* VHF and UHF LEDs: Not currently used, as of 2022-01-17.
* Display: It, uhh, displays stuff... See below.

Controls:
* PTT Button: Makes it go.
* Volume Knob: Save's your ears.
* Encoder Wheel, with Encoder Button.
  * Navigate menus (in conjunction with Back button)
  * Change values on the screen, when that value is selected by a Function button
* Back Button.
  * Navigate menus (in conjunction with Encoder wheel and button)
  * Exit "change value" mode.
  * Push-and-Hold from anywhere to go to top menu and select the View.
* Five "Function" buttons
  * Action is dependent on context, and displayed on the screen.

## Function Buttons:
* PF1 is usually the "Func" button, which changes the action on the other buttons:
  * Normally, PF2 through PF5 do one action.
  * Push Func first, then PF2 through PF5 do another action.
  * Push-and-hold Func, then PF2 through PF5 do a third use.
    * **NOTE** You can also just Push-and-hold the PF button to do the same thing.
* Sometimes the Function Action does something immediately (such as switching from MR to VFO mode), sometimes it puts a cursor on a value on the screen (such as the function, or CTCSS tone) and allows you to change that value with the encoder wheel.  Accept the new value by pressing the Encoder Wheel button.

## Views
SOAR has several different "Views" for different actions:
* Standard HT, both VFO and MR (Memory) modes:  No special satellite operations, just operates like an HT.
* Satellite Pass Prediction: Lists the satellites that SOAR knows about, and their upcoming passes.
* Satellite Pass Operation: For working a satellite. Frequency is automatically doppler shifted, Azimuth and Elevation are displayed, audio is recorded, etc.
* Satellite Pass Replay: Replay's the audio of a previous pass operation, and displays what was on the screen at the time.
* Configuration Menu: Adjust the settings of SOAR.

### Switching Views
To switch between views:
* Push-and-hold the Back button.  This will take you to the Top Menu.
* Use the Encoder Wheel to select the View you want.
* Press the Encoder Button (push in on the knob) to enable the selected View.

### Header (Common to all Views)
The top row of the display is always there.  It displays:
* Time in UTC.
  * If the GPS is not sync'd yet, will display all zeros.
  * Future: Select a time zone to display instead.
* Grid Square, or GPS Sync Indicator.
  * If the GPS is sync'd, it will be a Green background and display the current 6 character grid square.
  * If the GPS is not yet sync'd, it will be a Red background and just display "GPS".
* Radio Indicators, `V` for VHF, `U` for UHF.
  * White on Black: The radio idle.
  * Green: The radio is receiving.  The Squelch is open, and the receive CTCSS tone (if specified) is detected.
  * Yellow: The radio is transmitting.
  * Red: There was a communication error with the radio. Reboot SOAR.
* View: The four letter short name for the view on the rest of the screen.  Such as `VFO`, `MR`, or `QSO`.
* Spinner.  Just an indicator that the microprocessor hasn't locked up.  The spinning is only based on time, not on any other hardware or software.  You can safely ignore it, unless it stops spinning.

### Standard HT, VFO mode: `VFO`
Displays:
* Frequencies, receive and transmit.
  * PF2 changes Rx frequency, Func-PF2 changes Tx frequency. Highlights the frequency box with a Yellow border, change value with Encoder Wheel.  Accept new value by pressing the Encoder wheel.
  * Push-and-hold-PF2 sets Tx frequency to the current Rx frequency.
  * If the Offset is `Simp`, `+`, or `-`, then the Transmit frequency is gray'd out and calculated accordingly.
  * If the Offset is `Split`, then the Transmit frequency is white user editable.
* CTCSS tones, receive and transmit.
  * PF3 changes Rx tone, Func-PF3 changes Tx tone. Highlights the tone indicator with a Yellow border, change value with Encoder Wheel.  Accept new value by pressing the Encoder wheel.
  * Push-and-hold-PF3 sets the Tx tone to the current Rx tone.
  * If no tone is specified, then `None` (transmit) or `RF Sq` (receive) is displayed, and the value is gray'd out.
* Offset.  One of: `Simp`, `+`, `-`, or `Split`.
  * PF4 cycles through the 4 available options.
* Squelch value, as a bar graph.
  * PF5 highlights the Squelch bargraph with a Yellow border, change value with Encoder Wheel. Accept new value by pressing the Encoder Wheel.
* High/Low power indicator.
  * Func-PF5 cycles between High and Low power.
* VFO/MR indicator.  A quick-button to switch Views.
  * Push-and-hold-PF5 to switch between MR and VFO Views.


TODO:
* A way to set a channel in VFO mode, then program it into a Memory Channel.

### Standard HT, Memory mode: `MR`
Note that none of these values can be changed, except: Channel Number, Squelch, and High/Low power.  Note however that Squelch and High/Low power are part of the memory channel; if you change channels and come back, the squelch and power will be reset to the value in the memory.  If you change them manually, it is only a temporary over-ride.

Displays:
* Channel Name (12 character max), and Channel Number (1 to 255)
  * Press the `MemCh` PF button to change the Channel. It highlights the Channel Number with a Yellow border. Use the Encoder Wheel to change the channel.  It won't apply the new values to the radio until you select the Channel by pressing the Encoder Button.
* Frequencies, receive and transmit.  
* CTCSS tones, receive and transmit.
  * If no tone is specified, then `None` (transmit) or `RF Sq` (receive) is displayed, and the value is gray'd out.
* Offset.  One of `Simp`, `+`, `-`, or `Split`
* Squelch value, as a bar graph. This is displayed directly above the PF button used to change it.
* High/Low power indicator.  This is displayed directly above the PF button used to change it.
* VFO/MR indicator.  Push-and-hold Func, then press PF5 to switch between MR and VFO mode.

### Satellite Pass Prediction: `Pred`
Not implemented yet (2022-01-17)

### Satellite Pass Operation: `QSO`
Like the `MR` View, most of the data on this screen is read-only.  You can only change the Channel Number, Squelch, and High/Low power output.

Displays:
* Channel/Satellite Name, and Channel Number.
  * This View limits the available channels to only the Satellites (Channels that have TLE data associated with them).
  * There is currently (2022-01-17) a bug that if you're already in a non-satellite channel when you enter the `QSO` View, it stays on that channel even though there's no TLE data available. But as soon as you select a new channel, it will jump to the next Satellite in the channel list, and not let you go back to the non-satellite channel.
* Frequencies, receive and transmit
  * The large numbers display the Actual frequency, after doppler shifts have been applied.
  * Below the large numbers, the satellite's center frequency, and the current doppler offset, are shown individually.
* Current Azimuth and Elevation of the satellite, displayed both numerically and on a Sky Chart.
  * When the satellite is below the horizon, the Elevation number is negative.  The Sky Chart will show the satellite as a Red dot on the outside ring.
* High/Low power indicator.  This is displayed directly above the PF button used to change it.
* Squelch value, as a bar graph. This is displayed directly above the PF button used to change it.
  * When the Elevation transitions from a negative to a positive number, SOAR automatically opens the RF squelch to 0.  Similarly, when the Elevation transitions from positive to negative, SOAR automatically applies the RF squelch value from the memory channel.

### Satellite Pass Replay: `Play`
Not implemented yet (2022-01-17)

### Configuration Menu: `Conf`
Not implemented yet (2022-01-17)


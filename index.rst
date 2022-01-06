..
  Technote content.

  See https://developer.lsst.io/restructuredtext/style.html
  for a guide to reStructuredText writing.

  Do not put the title, authors or other metadata in this document;
  those are automatically added.

  Use the following syntax for sections:

  Sections
  ========

  and

  Subsections
  -----------

  and

  Subsubsections
  ^^^^^^^^^^^^^^

  To add images, add the image file (png, svg or jpeg preferred) to the
  _static/ directory. The reST syntax for adding the image is

  .. figure:: /_static/filename.ext
     :name: fig-label

     Caption text.

   Run: ``make html`` and ``open _build/html/index.html`` to preview your work.
   See the README at https://github.com/lsst-sqre/lsst-technote-bootstrap or
   this repo's README for more info.

   Feel free to delete this instructional comment.

:tocdepth: 1

.. Please do not modify tocdepth; will be fixed when a new Sphinx theme is shipped.

.. sectnum::

.. TODO: Delete the note below before merging new content to the master branch.

.. note::

   **This technote is not yet published!**

   This document describes what should be checked in the event of a seismic event, specifically while in undergoing nighttime observations.

.. Add content here.
.. Do not include the document title (it's automatically added from metadata.yaml).

.. _AuxTel Temperatures and Pressures: https://chronograf-summit-efd.lsst.codes:30828/sources/1/dashboards/14?refresh=Paused&lower=now%28%29%20-%2024h
.. _Auxtel Daily-Checkout Notebook: https://github.com/lsst-ts/ts_notebooks/blob/develop/procedures/auxtel/observation_procedures/DayTime-Checkout.ipynb


Introduction
============

Seismic events occur regularily in Chile.
Depending upon the timing and severity of the event, a different response may be required.
The AuxTel system is designed to survive a seismic events up to 0.4g of acceleration, which is a major (and rare) event.
As of the time of writing, there is no accellerometer system installed on the summit that actively monitors and measures the acceleration from seismic events.
It is possible to obtain the magnitude and approximate location of an earthquake via alert streams on the internet post-facto, but this is not sufficient.
The magnitude system is indicative of severity but numerous factors regarding the event (e.g. location, depth, time of shaking) directly affects the accelerations received on the summit and the amount of potential damage and therefore cannot be used as the only indicator.

This document breaks down the procedures according to a qualitative on-site assessment of the severity.
The procedure should be followed starting from the greatest severity experienced, then following the sections written for less severe events until the system is fully recovered.

.. Important::
   In then event of ANY seismic event, operators should press the *TCS-Stop-All* button shown in :numref:`fig-ats-stop-all`.
   This will gracefully stop all observatory motion.

.. _fig_stop_all:

.. figure:: /_static/ATS-Stop-all.png
   :name: fig-ats-stop-all

   The button located in LOVE to rapidly stop all telescope and dome motion. 
   This button should be readily available and pressed by observers when experiencing and earthquake and will gracefully stop all motion.

Upon installation of the GIS, the E-stop will also be activated after several seconds, once the motion has ceased from the controlled stop above.
When the E-stop is activated, the brakes will engage and CSCs will go into fault state.
Recovery will require disengaging the E-stop using the `E-stop Reset Procedure <https://tstn-004.lsst.io/#e-stop-reset-procedure>`_. 

.. Note::
   For the code snippets found in this procedure, it is assumed you are running out of the `Auxtel Daily-Checkout Notebook`_ and have run the cells to instantiate the control classes.

.. _Severe_Earthquake:

Severe Earthquake
=================

This is a major (and rare) event.
Operators should press the *TCS-Stop-All* button shown in :numref:`fig-ats-stop-all` to gracefully stop all observatory motion.
For this level of earthquake (>0.2g) standing up and/or walking would be impossible. 
Moderate damage to equipment is expected.
Night time observations would be ceased and efforts would go into damage control and assessment.
The probability of network and/or power loss is high.

If the network goes down OR the power is out
--------------------------------------------

#. Do *not* attempt to move the telescope or dome azimuth.
#. Check the LATISS refrigeration system for leaks. 
   Warning, this gas is flammable (similar to propane).
   It will also have a strong odor (intentional safety feature).
   The leak will most likely occur near the white networking cabinet or close to the instrument.
   One can also check the gauge on the compressor located at the bottom of the white networking cabinet.

   * If a leak is found, immediately turn off the Polycold compressor, if possible, remove power to the 
     cabinet by turning off the breaker in the electrical cabinet (or just turn off all breakers for the building). 
     Leave building open to vent the gas and leave the area until the gas has completely evacuated.

     * If possible, disconnect the lines from the compressor AND from the rear of LATISS. 
       This requires the spanners designed for this task and should only be done by trained personnel.
       This will minimize the amount of released gas and help minimize damage to the refrigeration system.
  
#. Check copper air piping for leaks. An air leak will be noticed by sound (hissing), or by watching the pressure gauge on the air compressor. If a leak is found, turn off the compressor.

#. Close the mirror cover.
   It will close automatically with a loss of air pressure. 
   This can be performed by closing the valve at the compressor then disconnecting an air line.

#. If all power is off or the Polycold compressor is turned off due to a leak or damage, an uncontrolled warm-up of the instrument will begin to occur.
   If no leak has been found, or the gas has been vented, then get the turbo pump and connect it to the instrument.
   The internal cold trap should prevent damage, but if the turbo pump can be connected within 4 hours it will greatly reduce the risk of damage.

#. Check the vacuum of the dewar by looking at the number of lights illuminated on the ion pump. 
   If a warm-up is occuring, then turn off the ion pump using the toggle switch found on the silver box connected to the LATISS frame.

#. If inclement weather is approaching or the area is safe but non-functional, the main dome shutter should be closed. 

   * If the power is on, attempt to close the lower shutter, then the upper shutter, using the manual push buttons at the top of the stairs.
   * If the main power is off, there will be no power to the dome and the main shutter will need to be closed by hand.
     The lower shutter cannot be closed without a manual hydraulic pump.
     To manually close the top shutter, there is a large metal pole with a hook on the end found on the dome floor or in the shipping container on calibration hill.
     Attach the hook to the eye bolt near the motor shaft located at the very top of the dome.
     It will take ~5000 turns to close.


If the network stays up
-----------------------

.. Important::
   In the case of losing the main power AND the generator not coming online, this will mean that the AuxTel system is under UPS power and will only survive an hour or so (untested).
   The UPS can provide a small amount of power to protect the system, but dome rotation and shutter closure is not possible.

#. Do not attempt to move the telescope.
#. Check Vacuum Pressure
    
   * A spike to 1e-3 Torr may occur but should go down to ~7e-8 Torr or smaller after approximately 5 minutes.
     If this does not occur then the vacuum has been ruptured and the instrument must be warmed up immediately. 

   * The data can be found in the `AuxTel Temperatures and Pressures`_ Chronograf Dashboard.
   * If chronograf is down, the vacuum pressure can be checked if the ATCamera is enabled using::

      vacuum = await latiss.rem.atcamera.tel_vacuum.next(flush=True,timeout=5)
      print(vacuum.vacuum)
       

#. Check/monitor Polycold refrigerant supply and return pressures

   * The data can be found in the `AuxTel Temperatures and Pressures`_ Chronograf Dashboard.
     The values should smoothly follow the trend of the last 24 hours.
     Depending on when last filled and the temperature, the supply is between 1896054 and 2240792 Pascals (275-325 PSI), whereas the return varies around 448158 Pa (65 PSI).
   * If chronograf is down, the supply and return pressures can be checked if the AdamSensors CSC is enabled using::

      domain = salobj.Domain()
      adam_remote = salobj.Remote(name="AdamSensors", domain=domain)
      await adam_remote.start_task
      pressure = await adam_remote.tel_pressure.aget(timeout=5)
      pa_to_psi = 0.000145038
      print(f'supply pressure is: {pressure.pressure_ch3:0.0f} Pa, which is  {pressure.pressure_ch3*pa_to_psi:0.0f} PSI')
      print(f'return pressure is: {pressure.pressure_ch5:0.0f} Pa, which is {pressure.pressure_ch5*pa_to_psi:0.0f} PSI')


   * If the pressure is decreasing rapidly then there is a leak in the system.
     This will result in the instrument warming up.
     Warning, this gas is flammable (similar to propane).
     It will also have a strong odor (intentional safety feature).
     Power off everything in the cabinet immediately via the UPS.

     * If the leak is small, then the building can be entered and the hoses can be disconnected to minimize the leak. 
       This requires the spanners designed for this task and should only be done by trained personnel.
     * If the leak is large then the building should be fully vented as the gas is flammable.

#. Check if the ATMCS went into fault state. 
   If so, just leave it in fault, if not then transition it to standby.
#. Check if the ATPneumatics went into fault state. 
   The goal is to check the main line pressure for leaks, then close the mirror cover

   * If in fault, attempt to troubleshoot why this occurred. 
     Bring back into enabled state, no damage will be done by this.
     
   * Check the main line pressure (normally around 45-60 PSI); if it is low then a leak has occurred.
  
     .. code-block:: python

          pressure = await atcs.rem.atpneumatics.tel_mainAirSourcePressure.next(flush=True, timeout=5)
          print(f'Air pressure is {pressure.pressure:0.0f} Pascals.')

     * If not leaking:
  
       * Close the M1 mirror cover and vents::
         
          await atcs.close_m1_cover()
          await atcs.close_m1_vent()

       * Open the control loops::

          await atcs.rem.ataos.cmd_disableCorrection.set_start(m1=True, hexapod=True, atspectrograph=True)

       * Set the M1 pressure to zero to lower the mirror::

          await atcs.rem.atpneumatics.cmd_m1SetPressure.set_start(pressure=0)

     
     * If leaking:
  
       * The valve near the air compressor must be closed and the compressor powered off.
         This will automatically close the mirror cover and vents if the telescope is above ~50 degrees elevation.
         If not, the mirror petals might need a light push to close.
         Be sure to keep all fingers away from the edges of the petals

#. If inclement weather is approaching or the area is safe but non-functional, the main dome shutter should be closed. 

   * If the main power is on, attempt to close the lower shutter, then the upper shutter, using the manual push buttons at the top of the stairs.
   * If the main power is off, there will be no power to the dome and the main shutter will need to be closed by hand.
     The lower shutter cannot be closed without a manual hydraulic pump.
     To manually close the top shutter, there is a large metal pole with a hook on the end found on the dome floor or in the shipping container on calibration hill.
     Attach the hook to the eye bolt near the motor shaft located at the very top of the dome.
     It will take ~5000 turns to close.


.. Important::
   If the power is restored before the UPS runs out of battery power, and the vacuum and refrigeration system is not compromised, then LATISS will not require an emergency warm-up.
   If the power is off for too long and the pressure rises above ~5e-5, then an emergency warm-up is required.

.. _Moderate_Earthquake:

Moderate Earthquake
===================

This is relatively common occurance (several times per year).
Operators should press the *TCS-Stop-All* button shown in :numref:`fig-ats-stop-all` to gracefully stop all observatory motion.
For this level of earthquake (<0.1g) standing up and/or walking would be possible. 
Damage to equipment is possible but not expected.
Night time observations would be ceased temporarily but are expected to resume.
Power and networking is not disrupted.

#. Verify the vacuum and temperatures of LATISS are nominal via the `AuxTel Temperatures and Pressures`_ Chronograf Dashboard.

   * If a leak occurred, consider this a `Severe_Earthquake`_.

#. Perform a visual inspection of the building using the cameras in the building.

#. Verify no dome systems went to fault

   * If in fault state:

     * Check the error message, and also verify all systems look nominal in the engineering interface.
     * The dome will need to be manually inspected and motion should be verified using the manual push buttons prior to enabling the system.
       Unless bad weather is coming, first continue this list.


   * Turn off following mode from the ATCS and send the ts_domeTrajectory CSC to standby therefore ensuring no dome motion will occur automatically.
  
     .. code-block:: python

         await atcs.disable_dome_following()
         await salobj.set_summary_state(atcs.rem.atdometrajectory, salobj.State.STANDBY, settingsToApply='')

#. Verify that no telescope systems went to fault, specifically the ATMCS and ATPneumatics. 

   * It is very likely that the pointing component will go to fault state.
     This is expected behaviour so you can just re-enable the pointing component.
     
     .. code-block:: python

         await salobj.set_summary_state(atcs.rem.atptg, salobj.State.ENABLED)

   * If either system ATMCS went into fault, identify the issue as to why, starting with the ATPneumatics.
     If the error seems innocuous (e.g. data from pointing component stopped), then attempt to re-enable the CSCs one at a time.
   * Check the main line pressure (normally around 45-60 PSI) to make sure no leak has arisen..
  
     .. code-block:: python

         pressure = await atcs.rem.atpneumatics.tel_mainAirSourcePressure.next(flush=True, timeout=5)
         print(f'Air pressure is {pressure.pressure:0.0f} Pascals.')

   * Close the M1 mirror cover and vents to protect the glass.

     .. code-block:: python

         await atcs.close_m1_cover()
         await atcs.close_m1_vent()

   * Close the AOS loops (M1, hexapod, atspectrograph).
   * 
     .. code-block:: python

         await atcs.rem.ataos.cmd_enableCorrection.set_start(m1=True, hexapod=True, atspectrograph=True)

   * Track in place for ~1 minute, and ensure no errors occur.

     .. code-block:: python

         mountPositions = await atcs.rem.atptg.tel_mountPositions.aget(timeout=5)
         await atcs.point_azel(az=mountPositions.azimuthCalculatedAngle, el=mountPositions.elevationCalculatedAngle, rot_tel=mountPositions.nasmythCalculatedAngle)

   * Track sidereal motion for 1 minute and ensure no errors occur

     .. code-block:: python

         mountPositions = await atcs.rem.atptg.tel_mountPositions.aget(timeout=5)
         coord = atcs.radec_from_azel(az=mountPositions.azimuthCalculatedAngle, el=mountPositions.elevationCalculatedAngle)
         await atcs.slew_icrs(az=mountPositions.azimuthCalculatedAngle, el=mountPositions.elevationCalculatedAngle, rot=mountPositions.skyAngle, stop_before_slew=False)

   * Perform a 1 degree slew, then a 5 degree slew, then a 10 degree slew and ensure no errors occur

     .. code-block:: python

        # 1 degree slew, watch out for limits and adjust offset signs appropriately
        az_offset = 1; el_offset = 1
        mountPositions = await atcs.rem.atptg.tel_mountPositions.aget(timeout=5)
        coord = atcs.radec_from_azel(az=mountPositions.azimuthCalculatedAngle+az_offset, el=mountPositions.elevationCalculatedAngle+el_offset)
        await atcs.slew_icrs(az=mountPositions.azimuthCalculatedAngle, el=mountPositions.elevationCalculatedAngle, rot=mountPositions.skyAngle, stop_before_slew=False)

        # 5 degree slew, watch out for limits and adjust offset signs appropriately
        az_offset = 5; el_offset = 5
        mountPositions = await atcs.rem.atptg.tel_mountPositions.aget(timeout=5)
        coord = atcs.radec_from_azel(az=mountPositions.azimuthCalculatedAngle+az_offset, el=mountPositions.elevationCalculatedAngle+el_offset)
        await atcs.slew_icrs(az=mountPositions.azimuthCalculatedAngle, el=mountPositions.elevationCalculatedAngle, rot=mountPositions.skyAngle, stop_before_slew=False)

        # 10 degree slew, watch out for limits and adjust offset signs appropriately
        az_offset = 10; el_offset = 10
        mountPositions = await atcs.rem.atptg.tel_mountPositions.aget(timeout=5)
        coord = atcs.radec_from_azel(az=mountPositions.azimuthCalculatedAngle+az_offset, el=mountPositions.elevationCalculatedAngle+el_offset)
        await atcs.slew_icrs(az=mountPositions.azimuthCalculatedAngle, el=mountPositions.elevationCalculatedAngle, rot=mountPositions.skyAngle, stop_before_slew=False)

   * Stop tracking.

     .. code-block:: python

         atcs.stop_tracking()
  
#. Verify Dome CSC functionality (if dome was not in fault state or manual inspection and test passed)
   * Enable the dome CSC
  
     .. code-block:: python

         # This will use a default configuration, change as required.
         await salobj.set_summary_state(atcs.rem.atdome, salobj.State.ENABLED, settingsToApply='')

   * Perform a 4 degree move in one direction, then back in the other, remember the dome may not be homed.
  
     .. code-block:: python

         dome_az = await atcs.rem.atdome.tel_position.next(flush=True,timeout=10)
         print(f'Dome currently thinks it is at an azimuth position of {dome_az.azimuthPosition}.\n Note the dome may not be properly homed at this time')
         d_az = 4
         await atcs.rem.atdome.cmd_moveAzimuth.set_start(azimuth=dome_az.azimuthPosition+d_az)
  

   * Repeat for a 10 degree move

     .. code-block:: python

         dome_az = await atcs.rem.atdome.tel_position.next(flush=True,timeout=10)
         d_az = 10
         await atcs.rem.atdome.cmd_moveAzimuth.set_start(azimuth=dome_az.azimuthPosition+d_az)

   * Repeat for a 90 degree move in the opposite direction
  
      .. code-block:: python

         dome_az = await atcs.rem.atdome.tel_position.next(flush=True,timeout=10)
         d_az = -90
         await atcs.rem.atdome.cmd_moveAzimuth.set_start(azimuth=dome_az.azimuthPosition+d_az)

   * Home the dome
  
        .. code-block:: python

            atcs.home_dome()

#. Enable the atdometrajectory CSC and turn on dome following, the dome should align with the telescope

   .. code-block:: python

      await salobj.set_summary_state(atcs.rem.atdometrajectory, salobj.State.ENABLED, settingsToApply='')
      await atcs.enable_dome_following()

#. Slew to nearby target (about 5 degrees away) and track for 1 minute

     .. code-block:: python

        # 5 degree slew, watch out for limits and adjust offset signs appropriately
        az_offset = 5; el_offset = 5
        mountPositions = await atcs.rem.atptg.tel_mountPositions.aget(timeout=5)
        coord = atcs.radec_from_azel(az=mountPositions.azimuthCalculatedAngle+az_offset, el=mountPositions.elevationCalculatedAngle+el_offset)
        await atcs.slew_icrs(az=mountPositions.azimuthCalculatedAngle, el=mountPositions.elevationCalculatedAngle, rot=mountPositions.skyAngle, stop_before_slew=False)


#. Slew to desired target and continue observing

.. _Minor_Earthquake:

Minor Earthquake
================

These events happen regularily and are not expected to cause equipment damage.
Operators should press the *TCS-Stop-All* button shown in :numref:`fig-ats-stop-all` to gracefully stop all observatory motion.
Network and power are expected to be uninterrupted.

#. Verify that no systems went to fault, specifically the ATMCS and ATPneumatics. 
   
   * It is likely that the pointing component will go to fault state.
     This is expected behaviour.
     Just re-enable the pointing component.
     
     .. code-block:: python

         await salobj.set_summary_state(atcs.rem.atptg, salobj.State.ENABLED)

   * If faults occur, see the procedure for `Moderate_Earthquake`_.

#. Verify the vacuum and temperatures of LATISS are nominal via the `AuxTel Temperatures and Pressures`_ Chronograf Dashboard.

   * If a leak occurred, consider this a `Severe_Earthquake`_.

#. Track in place for ~1 minute, and ensure no errors occur.

   .. code-block:: python

      mountPositions=await atcs.rem.atptg.tel_mountPositions.aget(timeout=5)
      await atcs.point_azel(az=mountPositions.azimuthCalculatedAngle, el=mountPositions.elevationCalculatedAngle, rot_tel=mountPositions.nasmythCalculatedAngle)

#. Track sidereal motion for 1 minute and ensure no errors occur

   .. code-block:: python

      mountPositions=await atcs.rem.atptg.tel_mountPositions.aget(timeout=5)
      coord=atcs.radec_from_azel(az=mountPositions.azimuthCalculatedAngle, el=mountPositions.elevationCalculatedAngle)
      await atcs.slew_icrs(az=mountPositions.azimuthCalculatedAngle, el=mountPositions.elevationCalculatedAngle, rot=mountPositions.skyAngle, stop_before_slew=False)

#. Slew and track to nearby target (~5 degrees away) and track for 1 minute and ensure no errors occur

   .. code-block:: python

      # 1 degree slew, watch out for limits and adjust offset signs appropriately
      az_offset=5; el_offset=5
      mountPositions=await atcs.rem.atptg.tel_mountPositions.aget(timeout=5)
      coord=atcs.radec_from_azel(az=mountPositions.azimuthCalculatedAngle+az_offset, el=mountPositions.elevationCalculatedAngle+el_offset)
      await atcs.slew_icrs(az=mountPositions.azimuthCalculatedAngle, el=mountPositions.elevationCalculatedAngle, rot=mountPositions.skyAngle, stop_before_slew=False)


#. Continue with standard observations.

.. .. rubric:: References

.. Make in-text citations with: :cite:`bibkey`.

.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa

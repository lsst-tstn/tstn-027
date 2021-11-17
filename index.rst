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

   This document describes what should be checked in the event of a seismic event, specifically while in undergoing observations.

.. Add content here.
.. Do not include the document title (it's automatically added from metadata.yaml).

Introduction
============

Seismic events occur regularily in Chile and depending upon the timing and severity of the event a different response may be required.
The AuxTel system is designed to survive a seismic events up to 0.4g of acceleration, which is a major (and rare) event.
As of the time of writing this document, there is no accellerometer system installed on the summit that actively monitors and measures the acceleration from seismic events.
The use of a the magnitude system is indicative of severity but numerous factors regarding the event (e.g. location, depth, time of shaking) directly affects the accelerations received on the summit.

This document breaks down the procedures according to a qualitative on-site assessment of the severity.
The procedure should be followed starting from the greatest severity experienced, then following the sections written for less severe events until the system is fully recovered.


Severe Earthquake
=================

This level of earthquake (0.2g) where standing up would be impossible. 
Moderate damage to equipment is expected.
Night time observations would be ceased and efforts would go into damage control and assessment.

If the network goes down OR the power is out
--------------------------------------------

#. Do *not* attempt to move the telescope or dome azimuth.
#. Check the LATISS refrigeration system for leaks. 
   Normally, this will be a foul odour caused by an odorant in the flammable gas (mostly propane). 
   The leak will most likely occur near the white networking cabinet or close to the instrument.
   One can also check the gauge on the compressor located at the bottom of the white networking cabinet.

   * If a leak is found, immediately turn off the Polycold compressor, if possible, remove power to the 
     cabinet by turning off the breaker in the electrical cabinet (or just turn off all breakers for the building). 
     Leave building open to vent the gas and leave the area until the gas has completely evacuated.

     * If possible, disconnect the lines from the compressor AND from the rear of LATISS. 
       This requires the spanners designed for this task and should only be done by trained personnel.
       Any leak must also be small.
  
#. Check copper air piping for leaks. An air leak will be noticed by sound (hissing), or by watching the pressure gauge on the air compressor. If a leak is found, turn off the compressor.

#. Close the mirror cover.
   It will close automatically with a loss of air pressure. 
   This can be performed by closing the valve at the compressor then disconnecting an air line.

#. If all power is off or the Polycold compressor is turned off due to a leak or damage, an uncontrolled warm-up of the instrument will begin to occur.
   If no leak has been found, or the gas has been vented, then get the turbo pump and get it ready to connect to the instrument.
   The internal cold trap should prevent damage, but if the turbopump can be connected within 4 hours it will greatly reduce the risk of damage.

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

#. Check/monitor Refrigerant pressure

   * If the pressure is decreasing rapidly then there is a leak in the system.
     Warning, this gas is flammable.
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
     
   * Check the main line pressure, if it is low then a leak has occurred.

     * If not leaking:
  
       * Close the M1 mirror cover
       * Open the control loops
       * Set the M1 pressure to zero to lower the mirror
     
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



Regarding AuxTel, the following should be checked:
#. Check piping for leaks.

.. .. rubric:: References

.. Make in-text citations with: :cite:`bibkey`.

.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa

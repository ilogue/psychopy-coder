.. _eyetracking:

Communicating with an Eyetracker
=================================================

PsychoPy has components that allow you to connect and communicate with eyetrackers directly from Builder - without any code! These steps will guide you through how to set up, calibrate, and record from your eyetracker.

Step one: Know Your Eyetracker
-------------------------------------------------------------

PsychoPy supports many of the commonly used eyetrackers, you can find out if yours is supported by following these steps:

* Click on the `Experiment Settings` icon (the one that looks like a cog, near the top left-hand side of the Builder window).
* Click on the `Eyetracking` tab:

.. figure:: /images/eyeTrackers.png

* The `SR Research` option is also known as `Eyelink`, so if you have an Eyelink device this is the option to choose.
* When you've found your eyetracker, just select it and click `OK`.
* If you want to test out your eyetracking experiment but don't have an eyetracker with you, you can select `MouseGaze`. This will allow your mouse cursor to act as a gaze point on your screen, and so allow you to simulate eye movements without using an eyetracker. Then, when you're ready to use your eyetracker, you can just select it from the Experiment Settings and run your experiment in the same way.

Step two: Set up your Eyetracker
-------------------------------------------------------------
When you've selected your eyetracker from the drop-down menu, a set of options that are specific to that device will appear, such as the model and serial number of your device. Here we will follow through with the MouseGaze options:

.. figure:: /images/mouseGaze.png

* Choose which mouse button you'd like to use to simulate blinks by clicking on the boxes.
* The `Move Button` option allows you to select whether PsychoPy monitors your mouse movement continuously, or just when you press and hold one of the mouse buttons.
* The `Saccade Threshold` is the threshold, in degrees of visual angle, before a saccade is recorded.


EyeLink
-----------
When setting up your EyeLink you will first need to make sure you have the following set up:

1. An "Experiment" computer (this is the computer the experiment is run on) - set the IP address of this computer to 100.1.1.2
2. A "Host" computer (this is the computer where the EyeLink software runs) - set the IP address of this computer to 100.1.1.1
3. In your PsychoPy Experiment Settings > Eyetracking ensure you have SR Research selected, in the IP address use 100.1.1.1 (the IP of the host computer).

Before any communication can happen between the eyetracker and your experiment, the two computers must be connected via an ethernet cable and you need to check the two devices can communicate with one another. You can check the connection by opening the command prompt/terminal on the experiment computer and typing :code:`ping 100.1.1.1` if the connection is successful you will see that the pings are successfully returned. If you have trouble connecting at this phase you will want to trouble shoot by searching the returned error message.

Sometimes different eyetracking systems will have their own set of "screens" or "protocols" that they present. These are independant of what we can currently control from PsychoPy, which means that if you have made your experiment using MouseGaze, then move to the lab with the EyeLink and change the eyetracker to SR Research the instructions that you see at the start of the calibration may appear a little different to what you were expecting!

The general protocol you will see is shown below.

.. figure:: /images/eyelink_calibration_flow.png

    The set of screens that will appear on your experiment presentation screen during calibration/validation, and what to press when.

Step three: Add Eyetracker components to your Builder experiment
--------------------------------------------------------------------
You can find the eyetracker components in the eyetracker component drop-down on the right-hand side of the Builder window.

* The first component to add is the **'Eyetracker Record'** component as this starts and stops the eyetracker recording. Usually, you would add this component to your instructions routine or something similar, so that your eyetracker is set off recording before your trials start, but you can add them in wherever makes sense for your experiment:

.. figure:: /images/eyeRecord.png

    You can choose whether you want this component to just start your eyetracker recording, just stop the recording, or whether you want the component to start the recording and then stop it after a certain duration.

.. note::
	If you've started the eyetracker recording at the start of your experiment, be sure to add in another eyetracker record component at the end of your experiment to stop the recording too!

* If you want to record information on gaze position, or you want your trial to move on when your participant has looked at or away from a target, you'll need to add in an **ROI component**. The ROI component has lots of options - you can choose what you want to happen when the participant looks at or away from a certain part of the screen, what shape your ROI is etc. All of which can also be defined in your conditions file, just like any other component. Choose the options that fit the needs of your experiment. Here, the component is set such that when a participant looks at a circular target for at least 0.1s (set by the min look time), the trial will end:

.. figure:: /images/eyeROI.png

* On the `layout` tab of the ROI component, you set the position and size of the ROI in the same way as you would set the position of any visual component:

.. figure:: /images/eyeROIPos.png

* It's also vitally important that you calibrate and validate your eyetracker. To do this, you will use two standalone components: **Eyetracker calibrate** and **Eyetracker validate**.
* These are a little different from other components in that they form a routine all on their own. You'll need to add them in right at the start of your experiment Flow.
* The **Eyetracker calibrate** component has all of the options you would expect from an eyetracker calibration:

.. figure:: /images/eyeCaliBasic.png
    :scale: 20%

    Set the basic properties of the calibration routine here.

.. figure:: /images/eyeCaliTarget.png
    :scale: 20%

    Set the properties of the target on this tab.

.. figure:: /images/eyeCaliAni.png
    :scale: 20%

    This tab allows you to set the properties of the target animation.

* The **Eyetracker validate** component, you'll notice, is pretty much identical to the calibration component - that's because it will use the calibration information to present the same screen to the participant to cross-check the recorded gaze position with the calibrated gaze position.
* The Eyetracker validate component will then show the offset between the recorded and calibrated gaze positions. You'll want these to be as close as possible to ensure that your eyetracker is recording gaze accurately.


What about the data?
--------------------------------------------------------------------
* The eyetracking data from the ROI will be saved in your usual data file. Extra columns are created and populated by PsychoPy, depending on what you've asked to record.
* In the example below, the trial ended when a participant looked at a target on the screen. You can see what each column represents in the figure below:

.. figure:: /images/eyeData.png
    :scale: 20%

    The data output will vary according to what you've asked PsychoPy to record about gaze.

* PsychoPy also provides the option to save your eyetracking data as a hdf5 file, which is particularly useful if you are recording a large amount of eyetracking data, such as gaze position on every frame for example.
* To save eyetracking data as a hdf5 file, just click on the Experiment Settings icon, and in the 'Data' tab check the box next to 'Save hdf5 file'.


If there is a problem - We want to know!
-------------------------------------------------------------
If you have followed the steps above and are having an issue, please post details of this on the `PsychoPy Forum <https://discourse.psychopy.org/>`_.

We are constantly looking to update our documentation so that it's easy for you to use PsychoPy in the way that you want to. Posting in our forum allows us to see what issues users are having, offer solutions, and to update our documentation to hopefully prevent those issues from occurring again!
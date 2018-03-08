## Lightbeam - measuring performance of Swing look-and-feels

Project LightBeam is targeted at Swing look-and-feel developers that wish to test the performance of their libraries.

LightBeam has a collection of static and dynamic scenarios that are targeting different core Swing components and different interaction scenarios. The static scenarios create a number of components and then render the main frame onto an offscreen buffer. The dynamic scenarios run a number of typical interaction scenarios that involve changing the components or models.

To measure the performance of a specific look-and-feel - in this case Nimbus - run the following command:

`java -Dswing.defaultlaf=javax.swing.plaf.nimbus.NimbusLookAndFeel -cp ../drop/lightbeam.jar:../lib/jgoodies-forms-1.8.0.jar:../lib/jgoodies-common-1.8.1.jar org.pushingpixels.lightbeam.DynamicPerformanceSuite 10
`

This will launch the dynamic performance suite and run all the scenarios ten times (the parameter passed to the `main()` method). Do not interact with the app while it's running, and do not switch away to other apps on your machine.

As the suite runs, it prints out thread user time and thread CPU time spent on each scenario, with minimum, maximum, average and deviance listed:

`avg  365, min  306, max  428, dev 0.12         Buttons : Toggling selection on buttons`

`avg  246, min  196, max  398, dev 0.24         Buttons : Toggling enabled on buttons`

`avg  339, min  245, max  587, dev 0.26         Buttons : Changing text on buttons`

`avg  204, min  118, max  465, dev 0.56          Combos : Toggling enabled on comboboxes`

`avg  151, min  128, max  212, dev 0.18          Combos : Toggling editable on comboboxes`

`avg  109, min   62, max  415, dev 0.94            List : Scrolling large list`

`avg   51, min   48, max   56, dev 0.05            List : Moving elements in a large list`

With this, you can compare the performance of your look-and-feel with that of core / third-party libraries. You can also track performance improvements and regressions during the development cycle.

Here is the script I use for Substance:

`SUBSTANCE_VERSION=8.0.00-rc`

`TRIDENT_VERSION=1.5.00-rc`

`java -Dswing.defaultlaf=org.pushingpixels.substance.api.skin.SubstanceGeminiLookAndFeel -cp ../drop/lightbeam.jar:../../substance/drop/$SUBSTANCE_VERSION/substance-$SUBSTANCE_VERSION.jar:../../substance/drop/$SUBSTANCE_VERSION/trident-$TRIDENT_VERSION.jar:../lib/jgoodies-forms-1.8.0.jar:../lib/jgoodies-common-1.8.1.jar org.pushingpixels.lightbeam.DynamicPerformanceSuite 10`

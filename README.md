# AutoLISP
AutoLISP code for generating CAD objects for report creation. 

This project focused on processing laboratory analyses into autoLISP routines that could be run in CAD Civil 3D (2021 and 2022) to automatically generate layers, create mleaders with text, and format these objects in the appropriate industry style (as requested). This project specifically focuses on laboratory results of asbestos sampling: each layer is a different material sampled for asbestos, each mleader is a particular sample meant to be placed on the layout. The formatting describes whether the sample returned positive, negative, or trace. Each mleader is generated on the appropriate layer such that layers can be cleanly reformatted or toggled. 

* Create layers with appropriate names and coloration (indicating positive, negative, or trace). 
![Generate Layers](./gifs/AddLayers.gif)

* Create mleaders under their appropriate layers with the correct formatting. 
![Generate MLeaders](./gifs/AddMLeaders.gif)

* Recolor layers and mleaders already existing for specific samples/layers for which the laboratory results have been changed or updated. 

# How it Works
Once the LISP routines (in .scr, AutoCAD script files) have been generated, they can be imported into the appropriate CAD file in one of two ways:

1. In the project/page in which you would like to perform layer creation/mleader creation/recoloring, drag the .scr file from your file explorer into the open window.
2. In the open window, type .scr and enter. In the file navigation window, select the appropriate script and hit enter.

In both cases, the script will run through without need for manual input. 

# Usage
As stated above, these are used for automatically generating CAD objects en masse in AutoCAD Civil 3D (2021 and 2022). They were originally created because manual input of each of these layers and mleaders arrested valuable work hours, and the tedious task often led to errors. These auto-generated objects output the layers and mleaders in seconds and allow for engineers to spend their time arranging the report rather than copying in sample and layer names.

* The layer creation generator comes in two forms: 1) continuous linetype and 2) custom linetype. This is to allow for a more general layer creation script, as well as one that supports specialized linetypes often used by industry engineers to provide more specific detail in their layouts. 

* The mleaders script generates mleaders in a new column per layer, beginning at (-15,15) (specified in the original project scope, though this could be modified). As such, the mleaders are arranged in columns, allowing for easy visual separation between layers and clean mleader separation for easy interaction. 

* The recoloring script recolors all layers and mleaders separated by negative, positive, and trace samples. It is notable throughout the project that the layer assignment is dictated by the most extreme mleader assignment (for example, a layer containing one positive sample and two negative samples is positive). This is to express the highest amount of risk possible. As such, there can be negative samples within positive layers, etc. The layer and mleader reassignment ensures proper formatting, and allows engineers to perform retroactive formatting if they choose to work on the layout before the lab results return (such that the scripts can be generated only using the layer/sample names and set to all negative, and then can be recolored with the laboratory analyses). 

# Config
If custom linetypes (for layers) or mleader styles are used, they must be pre-configured in the CAD layout. 

Custom linetypes must be defined in the appropriate acad.lin or acadiso.lin files in the environment path (for imperial and metric, respectively). 

Custom mleader styles must be defined within CAD, under the mleaderstyles dialog. These can also be imported in by copying in a mleader of the given style anywhere into the project. It's also notable that within this project, one of the parameters was that each of the linetypes defaulted to negative (color 96), not color by layer. 
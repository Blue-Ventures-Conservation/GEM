# MMM_v1.0
Mangrove Mapping Methodology v1.0


----------------------------------------------------------------------------------------------------------
INTRODUCTION

The Google Earth Engine Mangrove Mapping Methodology (GEEMMM) 
tools is an intuitive, accessible and replicable approach which caters to a
wide audience of non-specialist coastal managers and decision makers.  
The GEEMMM was developed based on a thorough review and 
incorporation of relevant mangrove remote sensing literature and 
harnesses the power of cloud computing including a simplified image-
based tidal calibration approach. The GEEMMM has been designed 
specifically for the detection mangroves in coastal environments, and 
offers the ability to explore mangrove dynamics through the generation
of multiple yearly land cover maps. The GEEMMM tool is for anyone who is 
interested in exploring mangrove distribution at local or national scales, 
have a basic understanding of how to use Google Earth Engine, and are 
familiar with the basic principles of remote sensing. GEEMMM offers the
user the ability to export georeferenced images and land cover maps, 
supporting spatial data layers, graphs, and tables. A pilot study was 
conducted and published in the Journal of Remote Sensing, 
demonstrating an advanced application of the GEEMMM (LINK). 

The published manuscript not only demonstrates one application for 
GEEMMM, but also describes in detail the various parameters, options, 
outputs, and user-interface features included in the tool. The manuscript 
walks through the three modules that the code is currently separated 
into. Module 1, helps the user select the input imagery that will be used
for classification. In this first module, the user has several parameters to 
adjust according for their specific project requirement  (e.g. years of 
Interes, months of interest, cloud cover, etc.), but all of the imagery is
sourced from the Landsat program (Missions 4, 5, 7, & 8). Module 2 has 
two key components, first, to explore the spectral relationships between 
the classification reference area bands and indices values, and, second,
to perform the Random Forest classification. The spectral relationship
part of Module 2, is very user interactive, and includes the option to view
correlation matrices of the calculated spectral indices. After the 
classifications are complete error matrices and accuracy statistics are 
automatically produced for each output map. Module 3 is also comprised
of two main components, the first being an exploration of mangrove 
dynamics, automatically calculating loss, persistence, and gain over the
area of interest, and the second being a thorough qualitative accuracy 
assessments tool, allowing the user to systematically perform a qualitative 
analysis of the classification outputs.

Separate from the three foundational scripts of the GEEMMM code, there is 
also a ‘Functions’ folder. This folder contains some of the back-end support
code that is used by the GEEMMM tool. None of the scripts in this folder will 
produce any outputs or maps if run independently in Google Earth Engine.
They have been included here for transparency for the user, to be able to 
see how certain intermediate products are generated or statistics
calculated. The inclusion of these dependant scripts will be further 
discussed in the ‘OPERATION’ section.

The ‘OPERATION’ section of this document will also go into further detail 
on how to best run the GEEMMM for your own personal use. The most 
convenient way will be to follow the three hyper-links and use the captured
code. However, this Git repository can also be copied and saved as a 
scripts in your own personal Google Earth Engine script library. However,
the later of these two options is more complicated, but would allow the
user to better understand the GEEMMM functionality. 

Additionally, the GEEMMM tool is designed to be universally applicable to 
any location, globally where mangroves occur. However, it should be noted
that the pilot study, and subsequently the default parameters currently 
associated with the GEEMMM tool, focused on the South East Asian 
country of Myanmar (Burma).  While some of these parameters are location
agnostic, such as the percentage of allowable cloud cover, others, like the
coastal tidal zone, are very location specific. The code is well commented to
help aide in the determination of the best parameters to set before running, 
but it is important to remember how the default parameters were selected.

OPERATION

There are two methods to run the GEEMMM, follow the links below and run 
The scripts, or copy the entire tool into your personal Google Earth Engine
Script library. The first options is the easiest to execute, and least likely to
generate any errors. 
 
The three links below are associated with each of the three modules 
discussed above. Run them in order, and save the exports for each script
(ideally to your personal Earth Engine ‘Asset’ folder).

Module 1:
https://code.earthengine.google.com/497c195237c019e8ccea6cc46f477544?noload=true

Module 2:
https://code.earthengine.google.com/3eefa4622f0f223d4ae66d2645dbadaf?noload=true

Module 3:
https://code.earthengine.google.com/668243c548c1e7cb75954a416da1d249?noload=true

The other option for running the GEEMMM code is to copy each of the three
Module scripts, and each of the function scripts into individual scripts saved 
To you Earth Engine script library. The complicated part in this method is
maintaining the script dependencies’ locations. If the user chooses to 
run the GEEMMM tool in this manner, they will also need to change the
paths for each of the ‘require()’ functions, located near the top of each 
module’s script.  

Example: 

//The code will look like this
var known_ext =  require('users/yanchojo/GEEMMM_v4_1/:modules/known_mangroves');
var coastline =  require('users/yanchojo/GEEMMM_v4_1/:modules/coastline');

//Once you have copied and saved your version of the GEEMMM code
// It will look like this

var known_ext =  require('users/**YourUserName**/**TheNameYouSavedItAs1**');
var coastline =  require('users/**YourUserName**/**TheNameYouSavedItAs2**');

It will be important that you do not change the variable name and that you 
associate the correct script path with the corresponding variable. If this is
not done for all 13 function scripts the GEEMMM will not work properly, 
likely producing errors. The names of each function script are close to the
variable names that they were written for. If there is a mix up, look back at
the git page and reference the three module scripts.

The data inputs for the GEEMMM have both internal and external source options,
however, to perform the classification in Module 2, classification reference 
data must be provided. Because of the unique nature of land cover 
classifications, this must be provided by the user. A process to create CRD 
in Earth Engine is provided here by Google:
    https://developers.google.com/earth-engine/tutorials/community/drawing-tools#example_classification_with_user-drawn_geometries

FUNDING

GEEMMM was funded by Blue Ventures Conservation, with support from
the UK Government’s International Climate Fund, part of the UK commitment
to developing countries to help them address the challenges presented by
climate change and benefit from the opportunities. You may learn more about 
BVC at:    https://blueventures.org/

CONTACT

If there are discovered bugs or issues with the code, or with the directions
on how to use is, you can contact Dr. Trevor Jones:
    trevor@blueventures.org
    
LICENSING

The included software in this package is distributed under the GNU General 
Public License v3.0. See License document included in this package.

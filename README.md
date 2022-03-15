# GEEMMM_v1.1
# Google Earth Engine 
# Mangrove Mapping Methodology v1.1 

----------------------------------------------------------------------------------------------------------
## INTRODUCTION

The Google Earth Engine Mangrove Mapping Methodology (GEM) provides an 
intuitive, accessible and replicable tool which caters to a wide audience 
of non-specialist coastal managers and decision makers.  This tool reflects 
a thorough review and incorporation of relevant mangrove remote sensing 
literature, and harnesses the power of cloud computing,  including a simplified 
image-based tidal calibration approach. The GEM is freely accessible for 
non-profit use and runs on comprehensive and thoroughly commented code within 
GEE. 

The GEM is designed specifically to map multi-date mangrove distributions
and quantify dynamics anywhere in their global distribution. Currently 
available tools and methods fall short of fully utilizing the wealth of 
local expertise typically held by coastal managers - the GEM works 
towards filling this gap, helping to combine local expertise with GEE’s 
cloud computing capabilities. While not requiring advanced skills in 
remote sensing, geospatial analysis, or coding, the tool is designed with 
the assumption that users have basic computer skills and are familiar with 
the key steps in mapping mangroves and assessing dynamics.  
 
A pilot study (i.e., [Yancho et al. 2020](https://www.mdpi.com/2072-4292/12/22/3758)) 
published in a special issue on 
[“Remote Sensing in Mangroves”](https://www.mdpi.com/journal/remotesensing/special_issues/remote_sensing_mangroves) 
in the journal Remote Sensing demonstrates an application of the GEM for
the entire coast of Myanmar (Burma) - a global mangrove loss hotspot.  The 
published manuscript not only demonstrates one application for GEM, but 
also describes in detail the various parameters, options, outputs, and 
user-interface features included in the tool. The manuscript walks potential 
users, step-by-step, through the three modules which comprise the tool: 

#### Module 1: Defining the Region of Interest (ROI) and Compositing Imagery 

>This module helps the user to define customized Region of Interest (ROI) 
>boundaries, and select the input imagery to make multi-date (i.e., historic 
>and contemporary) composites. The user adjusts several parameters according 
>to their specific project requirements and preferences (e.g. years of interest, 
>months of interest, cloud cover, etc.). It is in Module 1 that the user can 
>choose to calculate a number of mangrove and non-mangrove specific spectral indices.
>All imagery is sourced from the Landsat archives (Missions 4, 5, 7, & 8). 

#### Module 2: Spectral Separability, Classifications, and Accuracy Assessment 

>This module enables the user to choose from the calculate spectral indices (from Module 1) 
>to use as classification inputs, explore the spectral relationships within and between 
>user-defined map classes, undertakes multi-date (i.e., historic and contemporary) 
>supervised classifications, and assesses land cover map accuracies. Exploring spectral 
>relationships is very interactive, and includes the option to examine correlation 
>between potential spectral indices and separability of classification reference areas 
>(CRAs) across all potential classification inputs. Following classification, 
>accuracy assessments are automatically produced for each output map. 

#### Module 3: Dynamics and Qualitative Accuracy Assessment (QAA) 

>This module uses multi-date mangrove maps to automatically calculate and 
>subsequently explore mangrove dynamics (i.e., loss, persistence and gain), 
>and provides an optional qualitative accuracy assessment (QAA) tool. The 
>QAA goes above and beyond standard accuracy metrics.  

Separate from the three modules of the GEM, there is also a ‘Functions’ 
folder which contains some of the back-end support code used by the tool. 
None of the scripts in this folder will produce any outputs or maps if run 
independently in GEE. These scripts have been included for potentially 
interested users to understand how certain intermediate products are 
generated or statistics calculated. The inclusion of these scripts is 
further discussed in the ‘OPERATION’ section of this document (below), 
which also provides further detail on how to best run the GEMv for your 
own personal use. The most convenient way will be to follow the three 
hyper-links and use the captured code. However, this Git repository can 
also be copied and saved as scripts in your own personal GEE script 
library. The latter of these two options is more complicated, but would 
allow the user to more comprehensively understand GEM functionality - 
this is not required to actually use the tool.

For new users to GEE, there are several sources available to learn how the 
service works. The GEM has been designed to minimize knowledge requirements
for coding as much as possible, but it may be useful to familiarize oneself 
with the Earth Engine Javascript interface before use. The best resources 
available to new users are the [‘JavaScript and Python Guides’](https://developers.google.com/earth-engine/guides) 
provided by the GEE team. These guides walk the user through the basic elements 
of GEE. The [Earth Engine API](https://developers.google.com/earth-engine/apidocs)
documents also provide further information on GEE specific functions, and their 
associated variables and inputs. GEE also has a 
[large spatial data library](https://developers.google.com/earth-engine/datasets) 
available to users wherein users can find specific datasets they wish to use in 
the GEM, or learn more about default datasets available to GEM users. 
Another valuable resource for GEE users, new or experienced, is the GEE group, 
[“Google Earth Engine Developers”](https://groups.google.com/g/google-earth-engine-developers).
It is likely that most casual users of the GEM will not encounter issues that 
require the GEE community’s support, but the Google group is a useful resource 
if users begin to develop their own code. There are several common server-side 
errors which users may encounter while using the GEM. Please read the ‘KNOWN 
ISSUES’ section of this document before contacting the developers.

The development of the GEM was undertaken using the latest versions of both
Google Chrome (v98.0.4758.82) and Mozilla Firefox (v97.0) web browsers, on 
both macOS (v10.13.6) and Windows (v10.0.19042.610) operating systems. The 
functionality of the GEM on Linux systems or other web browsers is unknown at
this time. There have been some documented time-out errors related to non-Chrome
based GEE execution; more information on this problem can be found below in the
'Known Issues' section of this document.

Additionally, the GEM is designed to be universally applicable to any location, 
globally, where mangroves occur. However, it should be noted that the pilot study,
and subsequently the default parameters currently associated with the GEM, 
focused on the Southeast Asian country of Myanmar (Burma). While some of these 
parameters are location-agnostic, such as the percentage of allowable cloud cover,
others, like the coastal tidal zone, are very location-specific. The code is well 
commented to help aid in the determination of the optimal parameters to set before 
running, but it is important to remember how the default parameters were selected.
Importantly, all parameters can be changed by the user to meet their needs - the 
Myanmar pilot serves as a beginning to end demonstration of how the tool works. 

## OPERATION
Before the GEM can be used, the user must request developer access to GEE. 
This can be done by following this [link](https://signup.earthengine.google.com/) 
and filling out a simple request form. Approval typically takes one or two business 
days. Once your Google account has been granted access to GEE, you can use the GEM.

GEE is free to use for academic and not for profit enterprises. For commercial 
applications, GEE offers paid commercial licenses: details [here](https://earthengine.google.com/faq/).
At this time, the GEM is not available for commercial use - interested parties 
should contact the authors to confirm this status. 

There are two methods to run the GEM:
1) Click on the links below and run the scripts. Clear instructions are
provided in the comments within each script; or
2) Copy the entire tool into your personal GEE Script library.

The first option is the easiest to execute, and least likely to generate any 
errors.

The three links below are associated with each of the three modules discussed 
above. Run them in order, and save the exports for each script (ideally to your 
personal Earth Engine ‘Asset’ folder).


#### Module 1: Defining the Region of Interest (ROI) and Compositing Imagery

>https://code.earthengine.google.com/754ab072586056251b0d589d99aee8c0?noload=true

#### Module 2: Spectral Separability, Classifications, and Accuracy Assessment

>https://code.earthengine.google.com/54e855b9fd3e09d50fae750414278c76?noload=true

#### Module 3: Dynamics and Qualitative Accuracy Assessment (QAA)

>https://code.earthengine.google.com/df22cc7d6fd985104f9c4250a541bf07?noload=true

The second option for using the GEM is to copy each of the three Module 
scripts, and each of the function scripts into individual scripts saved to 
your GEE script library. The complicated part in this method is maintaining 
the script dependencies’ locations. If the user chooses to run the GEM in 
this manner, they will also need to change the paths for each of the ‘require()’ 
functions, located near the top of each module’s script.

#### Example:

    //The code will look like this
    var known_ext =  require('users/yanchojo/GEM_LS9/:modules/known_mangroves');
    var coastline =  require('users/yanchojo/GEM_LS9/:modules/coastline');

    //Once you have copied and saved your version of the GEM code
    // It will look like this

    var known_ext =  require('users/**YourUserName**/**TheNameYouSavedItAs1**');
    var coastline =  require('users/**YourUserName**/**TheNameYouSavedItAs2**');

It will be important that you do not change the variable name and that you 
associate the correct script path with the corresponding variable. If this is 
not done for all 13 function scripts the GEM will not work properly, likely 
producing errors. The names of each function script are close to the variable 
names that they were written for. If there is a mix up, look back at the Github 
page and reference the three module scripts.

After you have opened the links or saved the GEM locally, there are detailed 
code-comment instructions at the beginning of each module and above each distinct 
section and step of each module. Be sure to carefully read, in full, the instructions
for each module. It is in these instructions where the user must identify input 
datasets, determine impactful variables, and understand how certain functions 
within the GEM will operate. Throughout each module, there are comments at the 
end of each distinct section and step identifying the end of the user inputs/instruction.

The data inputs for the GEM have both internal and external source options, 
however, to perform the classification in Module 2, classification reference areas 
(CRAs) must be provided. CRAs are points or polygons that represent target map 
classes across the region of interest (ROI), offering a representative sample of 
how the user would like the classifier to sort the input imagery’s pixels into map 
classes. For example, a typical mangrove map may contain water, mangroves, bare soil, 
and non-mangrove vegetation. The user-defined CRAs should comprise points or small 
polygon areas that represent each of these classes in the input imagery, which will 
then be used as training (and validation) data for the multi-date classifications. 
An overview of how to create CRAs in GEE is provided 
[here](https://developers.google.com/earth-engine/tutorials/community/drawing-tools#example_classification_with_user-drawn_geometries)
by Google; however, users may also create CRAs in stand-alone (GIS) software of 
their choice, and subsequently point the GEM towards these data.  Whether using 
the GEE interface or importing from elsewhere, coastal managers can capitalize on 
their intimate first-hand knowledge to derive representative CRAs.


## KNOWN ISSUES

The most common errors that may occur (outside of user variable/input errors) are 
server-side memory issues. While GEE is a free service, it does have its limits, 
chiefly the allocation of server space for user initiated tasks. These will often 
be expressed as time-out or memory capacity errors. Errors which occur while trying 
to visualize a layer in the GUI can often be overridden by zooming in/out and/or 
panning the frame slightly to reload the map layers. The visualization errors are 
typically non-critical errors. Below is a short list of common server-side errors:

    “Tile Error: Too many concurrent aggregations”
    “Tile Error: Earth Engine Capacity Exceeded”

Anecdotally, the issues that produce these errors are usually associated with
processing large areas. While developing the GEM it was determined that
GEE works more effectively when dealing with smaller extents, i.e.
regional rather than national areas of interest. When exporting
large areas it is possible that the user may run into a 12-hour timeout limit. If
this happens, the exporting task will fail at 12 hours and produce an error
message stating:

    “Error: Computation timed out”

Coupled with the upper limits of GEE, internet connectivity can also present a 
stability and run-time challenge when using the GEM; however, it remains much 
faster than standalone workstations, and once one portion of the GEM initiates 
it will continue even if internet connectivity is temporarily lost.  This means 
that intermediate data products - and the user’s progress - is effectively saved,
to an extent.  

The selected web-browser is known to have an impact on time-out errors. Google 
Chrome has proven to be the fastest and most reliable web browser to use with the 
GEM. It has been documented that Firefox will have trouble loading calculated 
objects before producing a time-out error. However, this problem can typically be 
resolved by simply re-running the script.

## FUNDING

GEM was funded by Blue Ventures Conservation (BVC), with support from
the UK Government’s International Climate Fund, part of the UK commitment
to developing countries to help them address the challenges presented by
climate change and benefit from the opportunities. You may learn more about
BVC at:    https://blueventures.org/


## CONTACT

If there are discovered bugs or issues with the code, or with the directions
on how to use the tool, you can contact Dr. Trevor Gareth Jones:
    trevor@blueventures.org

Please be sure to read the KNOWN ISSUES section of this document before
contacting the developers.

    
## LICENSING

The included software in this package is distributed under the GNU General
Public License v3.0. See License document included in this package.


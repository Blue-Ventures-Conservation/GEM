# GEEMMM_v1.0
<h1>Google Earth Engine Mangrove Mapping Methodology v1.0 1</h1>


----------------------------------------------------------------------------------------------------------
<h2>INTRODUCTION</h2>

The Google Earth Engine Mangrove Mapping Methodology (GEEMMM)
tool is an intuitive, accessible and replicable approach which caters to a
wide audience of non-specialist coastal managers and decision makers.
The GEEMMM was developed based on a thorough review and
incorporation of relevant mangrove remote sensing literature, and
harnesses the power of cloud computing including a simplified image-based
tidal calibration approach. The GEEMMM has been designed
specifically for the detection of mangroves in coastal environments, and
offers the ability to explore mangrove dynamics through the generation
of multiple yearly land cover maps. The GEEMMM tool is for anyone who is
interested in exploring mangrove distribution at local or national scales,
has a basic understanding of how to use Google Earth Engine, and is
familiar with the basic principles of remote sensing. GEEMMM offers the
user the ability to export georeferenced images and land cover maps,
supporting spatial data layers, graphs, and tables. A pilot study was
conducted and published in the Journal of Remote Sensing,
demonstrating an advanced application of the GEEMMM (LINK).

The published manuscript not only demonstrates one application for
GEEMMM, but also describes in detail the various parameters, options,
outputs, and user-interface features included in the tool. The manuscript
walks through the three modules that the code is currently separated
into. Module 1 helps the user select the input imagery that will be used
for classification. In this first module, the user has several parameters to
adjust according to their specific project requirement (e.g. years of
interest, months of interest, cloud cover, etc.), but all of the imagery is
sourced from the Landsat program (Missions 4, 5, 7, & 8). Module 2 has
two key components, first, to explore the spectral relationships between
the classification reference area bands and indices values, and, second,
to perform the Random Forest classification. The spectral relationship
part of Module 2 is very user interactive, and includes the option to view
correlation matrices of the calculated spectral indices. After the
classifications are complete, error matrices and accuracy statistics are
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
code. However, this Git repository can also be copied and saved as
scripts in your own personal Google Earth Engine script library. The later
of these two options is more complicated, but would allow the user to
better understand the GEEMMM functionality.

For new users to Google Earth Engine, there are several tools available to
learn how the service works. The GEEMMM has been designed to
minimize knowledge requirements for coding as much as possible, but
it may be useful to familiarize oneself with the Earth Engine Javascript
interface before using the GEEMMM. The best resources available to new
users are the [‘JavaScript and Python Guides’](https://developers.google.com/earth-engine/guides) 
provided by the Google Earth Engine team. These guides walk the user 
through the basic elements of Earth Engine. The
[Earth Engine API](https://developers.google.com/earth-engine/apidocs) 
documents also provide further information on the Earth Engine specific 
functions, and their associated variables and inputs. Earth Engine also
has a [large spatial data library](https://developers.google.com/earth-engine/datasets) 
available to users. Here users can find specific datasets they wish to use 
in the GEEMMM, or learn more about default datasets available to GEEMMM users.
Another valuable resource for Earth Engine users, new or experienced,
is the Google Earth Engine group, [“Google Earth Engine Developers”](https://groups.google.com/g/google-earth-engine-developers).
It is likely that most casual users of the GEEMMM will not encounter issues 
that require the Earth Engine community’s support, but the Google group is
a useful resource as users begin to develop their own code. There are
several common server-side errors which users may encounter while
using the GEEMMM. Please read the KNOWN ISSUES section of this
document before contacting the developers.

The development of the GEEMMM tool was undertaken using the latest
versions of both Google Chrome (v86.0.4240.111) and Mozilla Firefox
(v82.0.2) web browsers, on both macOS (v10.13.6) and Windows
(v10.0.19042.610) operating systems. The functionality of the GEEMMM
tool on Linux systems or other web browsers is unknown at this time,
but no compatibility issues are currently known or expected.

Additionally, the GEEMMM tool is designed to be universally applicable to
any location, globally, where mangroves occur. However, it should be noted
that the pilot study, and subsequently the default parameters currently
associated with the GEEMMM tool, focused on the Southeast Asian
country of Myanmar (Burma). While some of these parameters are location-
agnostic, such as the percentage of allowable cloud cover, others, like the
coastal tidal zone, are very location-specific. The code is well commented to
help aid in the determination of the optimal parameters to set before running,
but it is important to remember how the default parameters were selected.


<h2>OPERATION</h2>

Before a the GEEMMM tool can be used, the user must request developer access to 
Google Earth Engine. This can be done by following this [link](https://signup.earthengine.google.com/) and filling out a simple
request form. Approval typically takes one or two business days. Google 
Earth Engine is free to use for academic and not for profit enterprises, 
commercial applications will require special permission. Once your Google
account has been granted access to Earth Engine, you can use the 
GEEMMM tool.  

There are two methods to run the GEEMMM:
1) Click on the links below and run the scripts. Clear instructions are
provided in the comments within each script; or
2) Copy the entire tool into your personal Google Earth Engine Script
library.

The first option is the easiest to execute, and least likely to generate any 
errors.
 
The three links below are associated with each of the three modules
discussed above. Run them in order, and save the exports for each script
(ideally to your personal Earth Engine ‘Asset’ folder).

<h4>Module 1:</h4>

>https://code.earthengine.google.com/00a0c3c08646eaf05965dd2121beed77?noload=true

<h4>Module 2:</h4>

>https://code.earthengine.google.com/da2c8eb2d490fe26cb6c76509398d1c4?noload=true

<h4>Module 3:</h4>

>https://code.earthengine.google.com/1c45d88a5fce2cf518dbd5c556693ce2?noload=true

The other option for running the GEEMMM code is to copy each of the three
Module scripts, and each of the function scripts into individual scripts saved
to your Earth Engine script library. The complicated part in this method is
maintaining the script dependencies’ locations. If the user chooses to
run the GEEMMM tool in this manner, they will also need to change the
paths for each of the ‘require()’ functions, located near the top of each
module’s script.

<h4>Example:</h4>

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
the Github page and reference the three module scripts.

After you have opened the links or saved the GEEMMM locally, there are detailed 
code-comment instructions at the beginning of each script. Be sure to carefully read,
in full, the instructions for each module. It is in these instructions where the user must
identify the input dataset, determine impactful variables, and understand how certain
functions within the GEEMMM will operate. There is a note at the end of each introduction
section identifying the end of the user inputs/instruction.

The data inputs for the GEEMMM have both internal and external source options,
however, to perform the classification in Module 2, classification reference
data (CRD) must be provided. CRD are points or polygon areas that represent 
unique land cover classes across the region of interest, offering a representative
 sample of how the user  would like the classifier to sort the input imagery’s pixels 
into land cover map classes. For example, a typical mangrove land cover map would contain, 
water, mangroves, bare soil, and non-mangrove vegetation. The input CRD should select 
points or small polygon areas that represent each of these classes in the input imagery, 
which will then be used as training (and validation) data for the land cover classification.
Because of the unique nature of land cover classifications, CRD must be provided by the user. 
A process to create CRD in Earth Engine is provided [here](https://developers.google.com/earth-engine/tutorials/community/drawing-tools#example_classification_with_user-drawn_geometries) 
by Google.    


<h2>KNOWN ISSUES</h2>

The most common errors that may occur (outside of user variable/input errors) are
server-side memory issues. While Google Earth Engine is a free service,
it does have its limits, chiefly the allocation of server space for user initiated
tasks. These errors will often be expressed as time-out errors or memory
capacity errors. Errors which occur while trying to visualize a layer in the GUI
can often be overridden by zooming in/out and/or panning the frame slightly
to reload the map layers. The visualization errors are typically non-critical errors.
Below is a short list of common server side errors:

    “Tile Error: Too many concurrent aggregations”
    “Tile Error: Earth Engine Capacity Exceeded”

Anecdotally, the issues that produce these errors are usually associated with
processing large areas. While developing the GEEMMM it was determined that
Earth Engine worked more effectively when dealing with smaller extents, i.e.
regional rather than national areas of interest. When exporting
large areas it is possible that the user may run into a 12-hour timeout limit. If
this happens, the exporting task will fail at 12 hours and produce an error
message stating:

    “Error: Computation timed out”


<h2>FUNDING</h2>

GEEMMM was funded by Blue Ventures Conservation, with support from
the UK Government’s International Climate Fund, part of the UK commitment
to developing countries to help them address the challenges presented by
climate change and benefit from the opportunities. You may learn more about
BVC at:    https://blueventures.org/


<h2>CONTACT</h2>

If there are discovered bugs or issues with the code, or with the directions
on how to use the tool, you can contact Dr. Trevor Jones:
    trevor@blueventures.org

Please be sure to read the KNOWN ISSUES section of this document before
contacting the developers.

    
<h2>LICENSING</h2>

The included software in this package is distributed under the GNU General
Public License v3.0. See License document included in this package.


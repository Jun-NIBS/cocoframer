# The cocoframer package
Functions for the Allen Institute's Mouse Common Coordinate Framework (CCF) in R.

### Functionality
cocoframer provides some limited funcitonality for using data from the Allen Brain Atlas that is registered to the Mouse Common Coordinate Framework.  

It currently assists:  
* Retrieving 3D, CCF aligned, gridded ISH data from the Allen Brain Atlas API  
* Rendering 2D plots of slices of ISH data  
* Retrieving the Mouse Brain Atlas structural ontology  
* Generating 3D plots of brain structures like those presented in the Allen Brain Explorer  

For additional data retrieval functionality beyond cocoframer, see the full Allen Brain Atlas API docs:  
http://help.brain-map.org/display/mousebrain/API  

For more information about the Allen Brain Atlas and the Common Coordinate Framework, see the Allen Brain Atlas website:  
http://atlas.brain-map.org/  

and the CCF documentation:  
http://help.brain-map.org/download/attachments/2818171/Mouse_Common_Coordinate_Framework.pdf  

An interactive, in-browser 3D structure viewer, the Allen Brain Explorer, is available here:  
http://connectivity.brain-map.org/3d-viewer?v=1

### Installation

cocoframer can be installed with:
```
devtools::install_github("AllenInstitute/cocoframer")
```

### Internet connection requirements

Some functions in cocoframer retrieve data from the Allen Brain Atlas API, and so require an internet connection.  

These functions are prefixed with `get_`.

### Examples

**Plotting a 3D brain structure**  

cocoframer includes 3D mesh objects from version 3 of the CCF (2017). These can be retrieved with cocoframer and plotted using the rgl package.  

In this example, we'll retrieve and plot the Hippocampal Amon's Horn (CA in the ABA structural ontology).
```
library(cocoframer)
library(rgl)

CA_mesh <- ccf_2017_mesh(acronym = "CA")

shape3d(CA_mesh)
```

**Plotting multiple 3D brain structures**  

To get some context, it's sometimes helpful to plot multiple structures.  

Here, we'll use a helper function included in cocoframer to plot the shell of the CCF (called root in the ABA structural ontology) with the CA:  
```
library(cocoframer)
library(purrr)
library(rgl)

structures <- c("root","CA")
mesh_list <- map(structures, ccf_2017_mesh)

plot_brain_explorer_structures(mesh_list,
                               fg_structure = "CA",
                               bg_structure = "root")
```

You can change the color and opacity of structures with additional parameters:

```
plot_brain_explorer_structures(mesh_list,
                               fg_structure = "CA",
                               fg_color = "orangered",
                               fg_alpha = 0.4,
                               bg_structure = "root",
                               bg_color = "yellow",
                               bg_alpha = 0.4)
```

### Common acronyms

These acronyms are used repeatedly in function names in cocoframer:  

aba: Allen Brain Atlas  
ccf: Common Coordinate Framework  
mba: Mouse Brain Atlas  
ish: In-Situ Hybridization  

### License

The license for this package is available on Github at: https://github.com/AllenInstitute/cocoframer/blob/master/LICENSE

### Level of Support

We are planning on occasional updating this tool with no fixed schedule. Community involvement is encouraged through both issues and pull requests.

### Contribution Agreement

If you contribute code to this repository through pull requests or other mechanisms, you are subject to the Allen Institute Contribution Agreement, which is available in full at: https://github.com/AllenInstitute/cocoframer/blob/master/CONTRIBUTION

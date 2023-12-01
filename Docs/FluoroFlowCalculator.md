# Fluoro Flow Calculator

## Summary

Module for measuring Qp-split using readily available fluoroscopy sequences.

To use the module, follow the following steps: 

1.	Import a DICOM file with a fluoroscopic sequence into Slicer (AP projection of an RV or MPA injection with good view of both lung fields and <20˚ RAO/LAO/CRA/CAU angulation). 
2.	Open the “Fluoroscopic Flow Calculator” module.
3.	Select the loaded fluoroscopic sequence as the input sequence.
4.	Select the start and end frames of contrast injection (from appearane of contrast in distal MPA up to start of levophase).
5.	Click “Create Segmentation” - this automatically splits the screen into 2 equally sized parts (or segmentations): ‘left’ and ‘right’ (Figure S1).
6.	Using the eraser tool from the built-in “Segment Editor” module - erase all areas with common blood pools (e.g. RA, RV, MPA). The rationale for this is that these areas contain blood with still undetermined destination – it can flow to perfuse either the right or left lungs, thus cannot be assigned to one specific side at this point in time.
7.	Click “apply”. 

The calculation of the relative perfusion is done automatically in the following manner: 
1.	For each image frame, get mean pixel intensity of pixels in each segmented region. Lower value of 0 correspond to maximum opacification, maximum value of 255 corresponding to no opacification. 
2.	Invert the scale so that 255 corresponds to maximum opacification (maximum contrast) and 0 corresponds to no opacification (no contrast). 
3.	Calculate the total contrast-level for each segmentation and each frame:
total segment contrast= total number of pixels in segment x mean(pixel opacification).
4.	Calculate the baseline contrast-level prior to injection using the mean of all frames prior to injection of contrast material. 
5.	Subtract baseline contrast-level from each frame during contrast material injection. 
6.	For each segment, calculate the total sum of contrast-level above baseline from the start of injection and up till the start of levophase. 
7.	 Calculate the relative perfusion for each lung using the following formulas: 
a.	Left Relative Perfusion = left total contrast / (left + right total contrast)
b.	Right Relative Perfusion = right total contrast / (left + right total contrast)

![](../FluoroFlowCalculator/Resources/Icons/FluoroFlowCalculator.png)

Figure – The screen is automatically divided into 2 (left and right) and then the user manually erases all areas with common blood pools. The tool only measures changes in contrast levels relative to baseline. 

## References

Barak-Corren Y, Herz C, Lasso A, Dori Y, Tang J, Long C, Long C, Callahan R, Rome J, Gillespie M, et al. Abstract 11609: Developing a Novel Method for Measuring Relative Lung Perfusion at the Catheterization Laboratory. Circulation (2023) 148:A11609–A11609. doi: 10.1161/circ.148.suppl_1.11609

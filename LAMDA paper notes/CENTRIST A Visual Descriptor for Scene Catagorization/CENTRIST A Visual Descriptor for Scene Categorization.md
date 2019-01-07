## CENTRIST: A Visual Descriptor for Scene Categorization

*Jianxin Wu, Member, IEEE, and James M. Rehg, Member, IEEE*

####  Summary

In this paper, we propose CENTRIST, CENsus TRansform hISTogram, as a visual descriptor for **recognizing places** and **scene categories**.    

We analyze these tasks and show that the descriptor needs to be **holistic** and **generalizable**. It also needs to **acquire structural properties** in the image while **suppressing textural details**, and contain **rough geometrical information** in the scene.   

Through the strong constraints among neighboring Census Transform values, CENTRIST is able to capture the structural characteristic within a small image patch. 

In larger scales, **spatial hierarchy** of CENTRIST is used to catch rough geometrical information.    

#### Desired Properties 

- Holistic Representation 
- Capturing the Structural Properties 
- Rough Geometry is Useful 
- Generalizability 

#### Census Transform (CT) and CENTRIST 

Census transform compares the intensity value of a pixel with its eight neighboring pixels. If the center pixel is bigger than (or equal to) one of its neighbors, a bit 1 is set in the corresponding location. Otherwise, a bit 0 is set.   

The eight bits generated from intensity comparisons can be put together in any order (we collect bits from left to right, and from top to bottom), which is consequently converted to a base-10 number in [0,255].   

Another important property of the transform is that CT values of neighboring pixels are highly correlated.  

The transitive property of such constraints also makes them propagate to pixels that are far apart.   

Finally, the Census Transform operation transforms any three by three image region into one of 256 cases, each corresponding to a special type of local structure of pixel intensities.    

#### Constraints among CENTRIST Components 

$$\sum \limits_{i \& 0x08=0x08} \overrightarrow{h}(i)\geq \sum \limits_{i \& 0x10=0} \overrightarrow{h}(i)$$

where $\overrightarrow{h}$ denotes the CENTRIST descriptor of any image and $0\leq i \leq 255 $.

The equation means that the number of pixels whose CT value’s bit 5 is 1 must be equal to or greater than the number of pixels whose CT value’s bit 4 is 0.

By switching 1 and 0, we get another equation:  

$$\sum \limits_{i \& 0x08=0} \overrightarrow{h}(i)\leq \sum \limits_{i \& 0x10=0x10} \overrightarrow{h}(i)$$

#### CENTRIST Encodes Image Structures 

#### Reconstructing Image Patches from CENTRIST Descriptors 

#### Spatial Representations 

CENTRIST can only encode global shape structure in a small image patch, in order to capture the global structure of an image in larger scales we propose a spatial representation based on the Spatial Pyramid Matching scheme.   

The image is resized between different levels so that all blocks contain the same number of pixels. CENTRIST in all blocks are then concatenated to form an overall feature vector. 

two different spatial representations:

- We use PCA to reduce the CENTRIST descriptor to 40 dimensions, which we call spatial Principal component Analysis of Census Transform (spatial PACT) histograms, or sPACT. 
- We use a bag of visual words model.

#### Limitations of CENTRIST 

- CENTRIST is not invariant to rotations or scale changes. 
- CENTRIST is not a precise shape descriptor. 
- CENTRIST ignores color information. 
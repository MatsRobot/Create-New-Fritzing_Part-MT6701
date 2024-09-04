# Create-New-Fritzing_Part-MT6701
Creating New parts in Fritzing is not straight forward and it took me a day to get it right, so this is my notes when I made a new Frtizing Part MT6701


There are a lot of instructions on the YouTube but none I could follow to create a new part for the MT6701 that was good enough for my project. In some cases, the InkScape software were a newer version and didn’t have the same functionality, in other cases, the fonts and colours that Fritzing accepts could not be replicated in the .svg file created by the vector software and the solution ended up to be saving the files as a different SVG file format.
So this is a comprehensive step by step instructions with example files of how to create a part from scratch in Fritzing.

The full instruction is in 'Fritzing New Parts.doc'

The main issue was using InkScape to save the correct file format when it comes to Font and Rendering and this is explained in details in the document.

The font issue is more likely the dimension and fill parameter which could be edited in the xml editor within Inkscape. If the font elements include dimensions in “px” units, it causes Fritzing to displayed the text at the wrong size. 

The FritzingCheckApp application can help with that. Running the svg file that was saved from Draw through the tool will cleanup a lot of the problems. However a quick fix is to delete the values of font-Size if in px and fill value.

You need to open the XML Editor (Edit – XML Editor) and delete the font-size in px.by clicking on the bin. The colour change may not work if it is fixed value in XML and you need to delete the line.

![Screenshot 2024-09-04 081233](https://github.com/user-attachments/assets/8f07b2f2-e7df-45d7-867e-32d66262723b)

The other issue is the fill colour that makes the text appear black in Fritzing regardless of the actual text colour viewed and saved in Inkscape and you need to delete it.

![Screenshot 2024-09-04 081324](https://github.com/user-attachments/assets/ec5d38ef-9503-4922-89c6-7b0aa8f70c04)



# This is the documentation for Me, Marwan Abbas, while working as an intern in Efabless. 

This documentation will document my journey from the beginning of the internship, till the end and everything I learned.

# Useful documentation

I developed two useful documentation files in this repository, to work with the OpenRAM, it is highly recommended to take a look at them, they will help a lot in understanding the OpenRAM and how it works

- CodeDocumentation.md: This is a document that has all the code documentation that you would need, it is devided into module names and each module has a few lines that describes what this module is used for

- documentation.md: This file discribes the OpenRAM on a higher level, this would be useful for a beginner developer working on the OpenRAM, and the user. It has more details than the readme file.

# Journey working with OpenRAM

In the beginning I didn't know anything about OpenRAM, I didn't even know what it's used for. By time I understood more and got to know the importance of OpenRAM in the future of Open Source. 

To get to know the OpenRAM I read the README file a lot, got to experiment with the technologies that are already in place in the OpenRAM, got to look at all the output files and understand what is happening. For anyone working on the OpenRAM, now with the documentation I provided along side with VLSIDA's documentation, I hope everything would be more interesting and clear.

I then started my journey with SkyWater 130nm technology, which was the part that I really got to learn how the OpenRAM works and I got to experiment with it to see if there are bugs in the code, and reporting it back to VLSIDA. Integrating a new technology with OpenRAM isn't a challenge, the challenge was because this technology is brand new and it doesn't have any documentation, so the simplest and smallest error would be hard to find and needs a lot of debugging.

Due to the fact that SkyWater was a brand new technology, we had to tweak all the tools in order to work properly with it. My suggestion would be to follow the script I wrote in the CodeDocumentation, in order to setup the environment and have all the new repos in place, as things change quickly. If you are part of the efabless community, you should always make sure that the Efabless tree has all the new updates for the tools you are using, if not please report it to Mohamed Kassem, the CTO of Efabless.

# Important Modules

Modules that I usually work with, and are the most problematic (Had the most bugs) were the .magicrc, this module would be under the technology's libs.tech/magic directory. If you want the exact one that I modified please ask permission to access my private repos and you will find a modified SkyWater repo that has a modified .magicrc. This modification works perfectly with SkyWater, and you would not find it in VLSIDA or Tim Edward's repo. 

Second module is the magic.py, which could be found in the compiler/verify directory. There is where the run_drc.sh, run_lvs.sh and run_pex.sh are written, these files can be found in the tmp file, and these are the files that runs the drc, lvs and pex. These scripts always needs changes and maintenance, so whenever you change anything in the run_drc.sh in the tmp file for example, and you found out that it is working fine, and you would like to hard code it into the compiler, you can do that through the magic.py.

Tech and Tcl files, these files are involved with Magic and ngspice, to make the tools compatible with the technology you are using, for more information and help, Tim Edwards would be the best one to reach out to, he helped me a lot in figuring out the bugs with the tools. Highly recommend seaking help in using these modules, as if you don't have previous experience with the tool would produce a lot of errors.

Two important scripts for abstarcting cells can be found in the design file in the repo, you can run these scripts with adding the path and name of the cell, this will produce an abstracted cell. After abstarcting the cell, use magic in order to make sure it doesn't have any DRC errors, all the bitcells in the OpenRAM needs abstarction, so in the design file I provided an abstarcted .mag file, that you can use for ```replica_cell_1rw_1r, row_cap_cell_1rw_1r, dummy_cell_1rw_1r, cell_1rw_1r``` This would decrease the DRC errors.

For characterization of the sram, I had to make sure that the sram.sp produced in the tmp file has no bugs, one of the bugs was the units, the ngspice doesn't like the units. Another bug was a device that wasn't predefined, which should've been commented out in the characterization but it wasn't. These bugs are now fixed, but I just mentioned them for future reference.

###**Converting from Eagle to KiCad.**


* The following 4 **ulp** (Eagle user script file) and one **ulp** include file, work in together or stand alone too converts **Eagle**  *sch/lbr's* version 6.xx file(s) to **KiCad** *sch* and *lib/mod* files.  

* The Programs will do
	* Eagle multi sheet sch to KiCad  multi sheets.  
	* Global and local net labels for multi sheets.  
	* Multi part gates.  
	* Build KiCad PCB modules and SCH libs from Eagle SCH.  
	* Make project director to store all the converted files.  
	* And basic error checking.  
	* Eagle 6.xx PCB files can be directly import to KiCad.  

* By using the  the following **ulp's**  a consistent link from the SCH to PCB is maintained So forward and backwoods net-list annotation work's under KiCad!  

###Installing.
* Download the zip file, (*click on the Button to the your bottom right on this page*. **Download ZIP**) And unzip using your favorite zip program to your target directory. *OR* if your prefer git

			git clone https://github.com/lachlanA/eagle-to-kicad.git  

* **WARNING:**  The ULP's file-name will conflict with Eagles ULP's file-name's so  
	***DO NOT install them in Eagle's ULP directory***.  

* There are 4 **ulp's** and one **ulp** include file have been hack together.  
***renumber-sheet.ulp*** .......................   stage 1:  Add missing number(s) to parts Prefix's.  
***eagle6xx-sch-to-kicad-sch.ulp*** ....   stage 2:  Build sch and project files, etc  
***exp-lbrs.ulp*** .......................................   stage 3: *automatically runs*  Extract libs from Eagle SCH/PCB  
***eagle-lbr2kicad-1.0.ulp***..................  stage 4:  *automatically runs* Convert Eagle lbr to KiCad lib/mod  
***eagle_to_kicad_include.inc*** ...........  Include file used by the other 4 ULP's__ 
####HOW TO RUN THE ULP'S 
 
**WARNING Always backup your Eagle SCH/PCB files before running this program!**  

* **1:** Start your Eagle program *(Make sure your using  version 6.xx of Eagle)*

* **2:** Open the Eagle SCH/PCB  file you wish to convert. Make sure the Eagle SCH and PCB file's are both, Correct and pass all ERC/DRC checks in Eagle.  

* **3:** Next Open  the top left hand  **File menu** and select  **Run ULP**  

* **4:** A file requester window will open.  Using this, to select find or type the location of the ***renumber-sheet.ulp*** ULP you download from this website. We use this script to make sure all part prefix's are ending in a number  IE:   R0,  X1   etc. As KiCad will ask to renumber any prefix which dose not end in a number. *(It may do this any way, but don't worry it wont change any Prefix's which have already been numbered unless you tell it too!)*  Keeping prefix's consistent from SCH to PCB will allow net-list forward and back annotation to work in KiCad. Select **OK** *(this will run the scrip)*.  When this completes all references with out a number, should have a number appended to them. Note: This number will start from the largest reference number on the SCH/PCB.
        
* **5:** Next Open  the top left hand  File menu and select Run ULP  
Using this, to select the location of the ***eagle6xx-sch-to-kicad-sch.ulp*** you downloaded. Select OK *(this will run the scrip)* There are many options most most should just work OK. Make sure you make/select a ***clean target directory*** where all the KiCad file's will be put. Select OK, And with luck you should have SCH part done.   The previous ULP will link automatically to ***exp-lbrs.ulp*** for the  next step: If you have selected extract the KiCad lib's from Eagle SCH/PCB *(The default).* This  ULP will build  Eagle lbr file,  *Note: this can be a very slow process,  and will  
leave the Eagle PCB editor window open when complete*. Just ignore this for the moment. If this complete OK, the previous ULP will link to ***eagle-lbr2kicad-1.0.ulp*** which will convert the Eagle lbr file to a KiCad lib/mod file's.  The ***eagle-lbr2kicad-1.0.ulp*** window window will open with quite a few options. Just select OK for the moment.  And if *Murphy's Law  is sound asleep* we should have the target directory with all the converted files, including KiCad project files. But with one exception, it will be missing KiCad PCB file.

* **6:** For this, we need to Open KiCad's **pcbnew** program directly,  at the command prompt.
 *If you make the mistake of not opening **pcbnew** directly, and instead chose to run it from KiCad's **pcbnew**  menu. You will have no option for importing the Eagle 6 PCB file!*  Click on **File->Open** in **pcbnew** an window will pop-up, and on Wright side you will have a drop down menu box option, to select the type in import file. Select version 6.x  XML  of Eagle, and the PCB Eagle file linked to the Eagle SCH file we used at the beginning and press OK. After importing the Eagle PCB file, (with out error's I hope). Do a **SAVE AS** to **PROJECTNAME.kicad_pcb** to the new target directory *(where you saved the output from to preceding ULP's too).* **PROJECTNAME** being the name you give to your project early on. All being well you should have a converted Eagle SCH-PCB correctly linked and referenced.

* **7:** Next step is to check the KiCad **SCH** and KiCad **PCB** are consistent for parts and nets.
Start **KiCad**, and open the project in the newly created target directory. Open the SCH file. And if it was converted from the single SCH file, you should have the **SCH** file in the display. Or multi sheet **SCH** file you will have a number of small box's spread across the page. Each one of those box's being a converted Eagle sub-sheet. Click on the first one and check for errors. All being good, click on Generate Net-list, and click OK. It may ask to Annotate the **SCH**. If so do the Annotation step. And then come back and click on Generate net-list. And Generate it.

* **8:** Next click on **CvPCB**, this assigness the PCB footprints with the SCH parts. Most likely you will get the
following warning: *Some of the assigned footprints are legacy entries (are missing lib nicknames). Would you like CvPcb to attempt to convert them to the new required FPID format? (If you answer no, then these assignments will be cleared out and you will have to re-assign these footprints yourself.)* Just click the yes button. And a window will open up listing all the part's and foot print's which it has assignmented. Under FILE menu click Save. And then File Close.

* **9:** Next Clink on **PcbNew** button on the top menu, and the PCB should open up.
Now click on the **NetList** and a window should open up, from there click on Read Current Net-list. All going well you should not have any extra parts added, and only a few warnings about changing net list names.  And you should be done.  Please check over the converted **SCH/PCB** as there are many things which can go wrong.  While I have tried to catch as many conversion problems, I expect there many still wating to be found. ***So check and triple check the results!!!***

* **NOTES:**   For more info on KiCad  http://www.kicad-pcb.org/display/KICAD/Installing+KiCad  
As KiCad is the process of major upgrade,  and enhancement  please be nice asking ? of the Development team.  I think you  will love the new Push and Shove router, that feature alone makes it worth while moving from Eagle to KiCad I hope the ULP's make the job a lot easier.




  


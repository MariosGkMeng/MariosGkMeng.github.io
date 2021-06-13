# simulation-dashboard

## NOTE
Tool with source code will be uploaded soon ;) 

## What am I looking at?

This is a flexible, highly automated post-processor that I created in order to alleviate my eyes and brain from constant clicking and watching code for many consecutive hours. Once I saw how much it helps me organize my work and understood its potential, I thought it'd be a pitty not to share it.

### Who is it for
This is a usefull tool for everyone that runs numerous simulations in a specific system (automotive simulations, dynamic systems etc) and wants to be able to seamlessly compare results and track signal changes with respect to parameter changes. 

I am not suggesting that such a thought is unique to myself. There are already decent post-processors out there. One of them is the Data Inspector of Simulink-MATLAB. However, similar to the latter, many are only available in certain simulation environments and often require payment. This tool is generic and can be merged with a large range of software.

### Integrations developed so far

1. Integration with MATLAB
2. Integration with Python
3. Integration with GAMS 

## Motivation

The main goals of this long-awaited tool are:

- To introduce human factors and aesthetics to simulation studies with platforms that do not come with lean and flexible post-processors in order to minimize errors, eye strain and gasps of tiredness associated with assessing, understanding and writing code for extended periods of time.
- To automate tasks related to simulation studies and simulation results organization and comparison.

It has been years since I wished to be able to

-  effortlessly navigate through numerous simulation results
	-  without having to search them with traditional and inefficient methods (such as folder searching, file searching, etc.)
	- without the need to manually write simulation logs by noting parameter variations by hand. For instance, say you need to investigate effects of parameters you set in a simulation. Imagine having to write “parameter1: 0 --> 1” by hand for every simulation and then having to write assessment on effect of that parameter change by hand every time!

- Minimize the strain in my eyes that is generated by going through code all day! No matter how much you like to code, a combination of asimplistic GUI with smart automations and coding only when necessary is so much more human-oriented than a command line (sorry command line fans).

Of course, if you happen to be working on an already developed software that offers an efficient and pleasing post-processor, you do not need this tool right now. But often you will need to work on projects in which you’ll need to develop scripts (or use someone else’s) that perform the calculations.

Why excel and VBA?

*“What?? VBA?? How are you still using this old-fashioned, limited programming language in 2021??”*

Ok, before you report me to the Gods of programming, don’t forget that as a user you most probably won’t need to open a single VBA script in the tool.

Since many years I needed to enrich my excel automation skills for a few projects until it became a frequent “weapon of choice”. I was astounded by the vastness of possibilities excel can offer, while making it easy to check large chunks of numbers in a clean way.

For me, excel IS, in a way, a programming language. It is not tailored to computationally intensive tasks and this is the reason that I opt to use it only for organizing files, work and make visualizations. Especially regarding visualizations, it is easy to connect simple function results with different colors and styles in excel, as well as with icons. For a person who knows how to program in VBA, excel can be transformed into an optimal user-specific GUI.

If you have never used excel in that way and are skeptical, trust me, it is worth the small effort to get yourself familiarized with some of its capabilities, at least for the scope of this tool. I tried to keep the need to modify VBA scripts to a minimum. You are, however, required to have knowledge on how to use excel without VBA.

In addition, I believe that one should prefer this tool from other means of creating apps, because coding in VBA and writing functions in excel is much easier than building web-based apps, or apps on languages such as C++ and Java. After all, this tool is meant to be used by simulation engineers, researchers and generally analyzers, not strictly by developers. It is, therefore, easier to manipulate code in an excel-based tool and tailor it to your needs, than a web-based Java app.

Do not forget that given the fact that VBA is a very old and widely used language, it is so easy to google-search solutions to problems and find more than one suggestion in various websites. The VBA community is very large and eager to provide help.

Last but not least, it is easy to create simple functionalities in excel, something that most people know how to perform, as opposed to better programming languages. 
  

---

[[1]](#_ftnref1) There is a possibility to integrate Python, Javascript and C# to excel. It is in my TODO list for further development for this tool to migrate VBA to Python scripting.

           

## Modes of operation

There are two possible operation modes for which this tool works.

· **“Mode 1”** is the mode in which the tool connects to a simulator that is capable of text-parsing (usually a scripting environment that engineers use, like MATLAB, or Python). Check Figure below.

<img src="https://user-images.githubusercontent.com/61937432/121778272-e8722c80-cb9e-11eb-948b-50a88353f2d3.png" width="450" height="300" />

· “**Mode 2**” the one in which the simulator is unable to parse text files. That is usually a closed-source software that comes with a GUI. Check Figure below.

 <img src="https://user-images.githubusercontent.com/61937432/121778312-05a6fb00-cb9f-11eb-84ff-6ef031dec15b.png" width="450" height="300" />     
   
# Start from blank project

## Control room

In the “control room” you can:

- Define new parameters and change their values
- Add notes to parameters than only appear when you click on them
- Trigger a simulation
- Save a simulation’s results
- Stop a simulation

A control room that contains a few variables looks like the one in the provided example.

## Set project paths

1. Go to “project_paths” sheet. Set the following paths:
	1. *“print parameter file”:** This is the path where the parameter file is printed, ready to be parsed from your simulator (applicable for Mode 1)
	2.  **“write trigger text file”:** This is the path where the trigger file is printed, ready to be parsed from your simulator (applicable for Mode 1). More on trigger file in ???.
	3.  **“dropbox_folder_linking”:** This is the path where the simulator prints some user-wanted information (such as deviations from a mean variable, computation time, etc). This user wanted information is set in a script inside the simulator


## Create a new parameter

Type in the name of the **parameter** (in the same way that it will be read from your simulator). Once written, it is automatically generated in the vault. The corresponding value should be written next to the parameter (at its right). Check the example file for clarification.  ==IMPORTANT NOTE==: **Parameters should ONLY be written in odd columns (e.g. “A”, “C”, “E”, etc) and never before row 6!**

The simulator obtains the parameters in a proper form. Since so far the supported simulators are MATLAB and Python, a convenient and organized way to parse parameters is via struct variables and dictionaries correspondingly. If, for instance, you create a parameter titled “mass” and set a value of, say, “100”, then if your simulator is: 
       
- MATLAB, the parameter file will include a line: “d.mass = 100;”
- Python, the parameter file will include a line: “d[“mass”] = 100”

           

Where “d” is the struct or dictionary variable that carries the parameters. You can change the name of that struct variable in the “parameter_map” sheet, cell “A2”, or variable “struct_name”.


## Create a  parameter family
   
To enhance organization of your parameters, you can create parameter categories, or “families”. To do so, simply write “fam__familyName (optional_field_name)”.

- Why write “fam__” before the name?
	- So far, the program I developed understands parameter families that way
- What is “optional_field_name”?
	- The parameters are written in a struct (if simulator is MATLAB) or dictionary (if simulator is Python). If in your code you want to further categorize some parameters and make it easy to read, you can have something like: “d.deb.set_to_zero_when_inf”. The field “deb” can be referring to debugging related, on/off type of parameters. In that case, you write“fam__debugging (deb)”. If you do not want such a categorization, simply set the family like this: “fam__familyName ()”.


## View and create notes on parameters

https://user-images.githubusercontent.com/61937432/121816212-02853b00-cc83-11eb-810b-8365b7eedf8c.mp4  

- If you select a parameter cell, its notes automatically pop-up
- To add a note, click on the "![image](https://user-images.githubusercontent.com/61937432/121778331-1f484280-cb9f-11eb-9845-9d2adbdd6483.png)" icon at the top of your current view
- To add a picture:
	- Copy the picture from your source
	- Paste it in the excel sheet (**NOTE**: **note view mode should NOT be on**)
	- Press the "![image](https://user-images.githubusercontent.com/61937432/121778335-24a58d00-cb9f-11eb-8952-f4708a094946.png)" icon (it basically attaches it to the group of notes that correspond to this parameter)

https://user-images.githubusercontent.com/61937432/121816860-b63bfa00-cc86-11eb-95c2-1ea8a28728bd.mp4

That way, you won’t need to navigate to other files in order to take notes on the effects of parameters. In addition, parameters can be linked to effects of specific metrics (say, “vehicle acceleration”, “fuel consumption” etc), and you can systematically document effects of parameters on metrics.



## Delete a parameter
           

Navigate to “**parameter_map**” sheet, column “C” (Picture ???). Simply go to the specific cell that contains that variable and press “Delete” from your keyboard. No need to insert anything in that list, since it is automatically generated. **NOTE: You can only delete one variable at a time. Also, you have to delete that variable from the “control_room”. This command deletes all the notes of that parameter****.**

![image](https://user-images.githubusercontent.com/61937432/121778346-2e2ef500-cb9f-11eb-9ec5-93091365ce72.png)

## Run simulation in mode 1  

Find supported simulators (developed so far) in _Appendix_.
            

Steps (for MATLAB, more simulators to come in the future):

1. Run the “autorun.m” script in your MATLAB that reads the autorun file every (e.g., every 500ms). Leave that script running, **do not interrupt it**! You will have to edit this script first, to set which scripts/functions should run for each different event/trigger.

2. Go to the user interface --> "control_room" sheet and choose an action:

- Pressing “![image](https://user-images.githubusercontent.com/61937432/121778354-35560300-cb9f-11eb-8e9a-8011e801738d.png)” icon runs a simulation with the specified parameters (excel writes to autorun file a trigger that is understood by the simulator parser, for instance: “RUN_SIM 1”. Simulator reads this and triggers the simulation process.

- Pressing “![image](https://user-images.githubusercontent.com/61937432/121778358-3b4be400-cb9f-11eb-992b-890c7b34e95e.png)” saves the simulation results. Press it only once the simulation is finished (more on that in section ???)
        
## Live Simulation dashboard – Check simulation data while simulation is running

Navigate to simulation dashboard by clicking the “![image](https://user-images.githubusercontent.com/61937432/121778366-456de280-cb9f-11eb-8fc9-47ff109ff992.png)” icon for the options to appear and then the “![image](https://user-images.githubusercontent.com/61937432/121778369-4acb2d00-cb9f-11eb-882f-1e86f8ebdfc3.png)” icon. As a default mode, some live results are parsed from a textfile when you click on a new cell.

In the example I provided for mode 1, MATLAB prints the computation time for each iteration and the word “PROBLEM” whenever a specific signal problem is encountered. In the live dashboard, the figure shows the CPU time of each iteration (blue curve) and whether a problem was encountered (red curve: 1 when “PROBLEM”).

To modify how the live dashboard works, you will have to change some cell equations in this sheet, so excel knowledge is required.

## Make your GUI more beautiful (to your standards of “beauty”)

Most people are not aware just how much you can achieve with excel. One of the things that is not common knowledge about excel is that you CAN easily make it look good. In this section, you will find some tips that help you make your dashboard easier to and more pleasurable to read.

Go to: View --> Appearance and deselect the boxes, so that you don’t have to always see those column letters and row numbers and equations that occupy your “eye space” when you don’t really need them.
![image](https://user-images.githubusercontent.com/61937432/121778386-5c143980-cb9f-11eb-8d9a-88ea7b0e11ee.png)

- Cell formatting --> Check “conditional formatting” on the internet 😉
	-  Format of parameter value bearing cells that contain formulas (so that you don’t just delete them).
- Copy the cell and paste as a connected icon. Then, each time the value and format of the cell changes, the same thing will happen to the icon.
- Flagging parameters with expressive icons
	- For parameters you consider critical for your results, you can have the GUI flag them with icons of your preference. Simply navigate to “parameter_map” sheet à “T5” cell and add the exact name of the parameter in the list (leave no empty cells between those parameters!). Once you go back to the control room, the icon will appear next to the parameter.
	- To change that icon, search for the icon named “potential_hazard__” in the “control_room” sheet, right click on it and select “change icon”.


## Parameter change and simulation history
          

https://user-images.githubusercontent.com/61937432/121816990-77f30a80-cc87-11eb-93a3-a24123879412.mp4


For me, this is the most important feature of the tool. Its capabilities are:

- Rigorous and easy organization of parameter changes (e.g., if I change parameter “m” from 50 to 100 in the “control_room”, the tool will automatically print: <dd/mm/yyyy> **m:** **50** **-->** **100**)
- Gather notes of each simulation (write it below the parameter change) and effects of parameters to specific signals and/or indexes. See Picture below for an example.
- 

<img src="https://user-images.githubusercontent.com/61937432/121778404-6a625580-cb9f-11eb-88c0-5fbf58797546.png" width="850" height="400" />



- Gather simulation results and have them available for the user when he/she wishes to view them. By pressing the “save sim” button at the control_room (after a simulation has been completed), the plots with the desired results are loaded to the “simulation_history” sheet. The user can view them by clicking once on the number of the simulation. See Picture below for an example. Information on how the simulator stores the results in Section ???.

![image](https://user-images.githubusercontent.com/61937432/121815755-a7524900-cc80-11eb-94c2-b4c232072a08.png)

Of course, upon preference you can apply the same functionality of integration between excel and your simulator and have your simulator, at the end of the simulation, show the plots. The script that prints lines in text files from VBA is very simple. Refer to the ??? script.
**NOTE: Whenever you create a new variable, simulation history also changes. If you do not want to keep those changes, simply navigate to the simulation history and manually delete them.**

## How the tool saves and stores simulation results
           
Again, this is up to you. The important detail to keep in mind is to maintain the continuity between the user interface and the simulator. They both organize the results using the prefix “@run” (for run 10, write "@run10"). I have placed a script titled “report_struct.m”, for the case that simulator is MATLAB.

## Trigger simulations from another device

It is possible to change the simulation parameters and trigger a new simulation from another device. I have chosen dropbox for this task, mainly for its simplicity and reliable connection to local folders.

To be able to use this functionality, first set the excel variable “trig_sim_dropbox” to 1 ([excel variables](https://www.techwalla.com/articles/how-to-use-variables-in-excel)). This commands the tool to scan the dropbox parameter excel file periodically and triggers a simulation if it encounters differences between parameters. Set this variable to 0 if you are not using this functionality, since it slows down the performance of the tool.

### Get feedback from a running simulation to another device
           

Not all devices can use VBA with excel (e.g., smartphones). So, it’d be best to be able to read some of the results (e.g., some live plots) by having the tool print them in a shared dropbox folder periodically.

1. Set the excel variable “repeat_read_sim” to 1. Set this variable to 0 if you are not using this functionality, since it slows down the performance of the tool.
2. charts, images: Get the name of the image or chart(s) you wish to export to the shared folder. Add this name to the “Charts to print to dropbox” category in the “project_paths” sheet. **Leave no blank cells between your inputs!**

## Simulate in Mode 2
If you are working on a project with a software that does not allow any coding, at least to the level of textfile parsing you applied to trigger a simulation, then there is another way.

An important prerequisite is to be able to at least use some textfiles, in the format of the specific software that you are using, in order to specify parameters (up to my experience, you can use both a gui and a text file to manipulate parameters for your simulation in a closed-source software).

You can use the parameter writing functionality of the excel tool to pass the parameters and variable names to your preferred programming environment (in case you don’t opt to use VBA) and generate a parameter file in the format that your simulator uses. That will require programming from your side since any different simulation software uses different formats.

The initiation of the task is identical to the one you have learned so far. You run the “auto_run” script. The difference here stems from the fact that instead of triggering a simulation in the same programming environment of the “auto_run” script, it prints the parameters in the simulator format. Meanwhile, the excel tool periodically checks the last-edited date of the simulator parameter file. Once it recognizes that this file has been modified, it directly opens the simulator to the user’s screen. At this point, the user triggers the simulation manually.

The excel tool periodically checks for production of result files (with already-known file names) and once it recognizes a most recent modification, it can trigger a script that parses those results and prints them in the tool.

## Comparing signals from different simulations-runs
           
If you have been working with a large number of simulations (so basically, a huge number of results), you might consider this functionality extra helpful.

Let’s say that you are running a large number of simulations and you need to visualize the effect of some parameters in specific signals. You can always perform this in MATLAB/Python. However, excel can offer a quick and more relaxed visualization of those effects, which works with a few clicks, instead of having to work with code (again).

### How it works
Whenever you save a simulation, the signals that are loaded to the excel tool are stored in another excel file (or csv). Navigate to simulation dashboard and click on the “![image](https://user-images.githubusercontent.com/61937432/121778218-b3fe7080-cb9e-11eb-8965-3c877b5f919f.png)” shape. To view the results of different runs, simply type in the run numbers (e.g., 10 for run10) below the “Run” cell. Notice that the parameters that have different values between those simulations immediately appear next to the plot (that is one of the essential goals of this tool, to be able to get that kind of information in a live manner, without the need for many clicks and display changes).

## Shapes

Shapes that act as buttons cannot be moved by left-clicking because left-clicking triggers their macro-script. To be moved, it must be selected with right click, then press “Esc” in order to close the right-click options, and then drag it with the left click in the desired new position.

**CAUTION:** Most shapes are not safe from accidental deletion!! If you happen to delete a shape, just close the sheet WITHOUT SAVING IT. Exceptions are:

- Flag type shapes: they are regenerated if the tool notices that one is missing

## Non-foolproof problems




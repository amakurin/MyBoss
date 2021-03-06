### What is MyBoss? ###
**MyBoss** is a tool for automatic organizational chart creation in PowerPoint on PC or Mac.

### Ok, how to run it? ###
If you use Windows — [click here to download the tool](https://github.com/devrazdev/MyBoss/raw/master/MyBoss.pptm). If you use Mac — scroll down to **How to run MyBoss on Mac?** section. 

### Ok, how to create an input file for it?
[Download the template file](https://github.com/devrazdev/MyBoss/raw/master/example%20input%20data.xlsx) and customize it. For details, scroll down to **How to create input file?** section.

---

### How do these org charts look like? ###
The slide below was automatically created with **MyBoss** using [example input data].

![MyBoss-demo](https://github.com/devrazdev/MyBoss/raw/master/misc/demo.gif)

[example input data]: <https://github.com/devrazdev/MyBoss/raw/master/example%20input%20data.xlsx>
[sample data]: <https://github.com/devrazdev/MyBoss/raw/master/sample%20input.xlsx>
[product demo]: <https://www.youtube.com/watch?v=Do3c5ff7b1c>

### Why should I use it? ###
There is a steadily [growing] interest in creating org charts, and the most [common] approach is creating them in PowerPoint manually, but, starting from ~50 people it becomes too time-consuming. Once you start [searching] for automation software, you discover [Microsoft Visio]. Indeed, Visio lets you visualize org structures of any size by uploading existing data and automatically arranging shapes, but it has 2 issues:

1. Visual appeal. Automatic charts look clumsy, they usually require manual adjustments
2. Flexibility. Visio org charts can't be natively pasted/edited in PowerPoint, so you get locked on Visio

Org chart automation has already become a feature of many cloud applications (ex. [Google Sheets], [OrgChartNow], [Lucidchart]). None of them have good chart appeal and very few allow export to PowerPoint. **MyBoss** creates beautiful org charts out of the box, and it's native for Microsoft Office suite. 

[growing]: <https://trends.google.com/trends/explore?q=create%20org%20chart&date=all>
[common]: <https://www.youtube.com/results?search_query=create+org+chart>
[searching]: <https://support.office.com/en-us/article/create-an-org-chart-in-office-9419815f-0d7f-4d8b-8220-822036b1fe2b>

[Microsoft Visio]: <https://products.office.com/en-us/visio/flowchart-software>
[Google Sheets]: <https://www.bettercloud.com/monitor/the-academy/create-an-org-structure-chart-in-google-sheets/>
[OrgChartNow]: <https://www.orgchartpro.com/products/orgchart-now-2/>
[Lucidchart]: <https://www.lucidchart.com/pages/how-to-make-an-org-chart>

### What are the main features of MyBoss? ###
- Automatic validation of data input (verifying there are no reporting loops, duplicate rows, typos, etc.)
- Automatic calculation of headcount statistics (employees per manager, direct reports per manager, etc.)
- Automatic selection of all chart parameters (sizes of cards, amount of white space between elements, distribution of parts of organizational structure per slides)
- Automatic creation of organizational charts of any complexity (just 1 click after data import)
- Automatic cross-linking of slides for easy navigation during presentation

And more:
- Manual mode to create organizational charts of custom design
- Customizable design, requiring no coding
- Clickable elements — **MyBoss** automatically detects the name of employee once you click on his/her card

Extended [product demo] is available on Youtube. 

### How to create input file? ###
To create your own input file, you need to fill the Excel template, following these basic rules:

1. One tab - one org tree.
2. One line - one employee.
3. "Must have" fields for CEO (boss, head of org tree):
    - Employee Surname
    - Employee Name
4. "Must have" fields for every other employee:
    - Employee Surname
    - Employee Name
    - Reports To Surname (manager's surname)
    - Reports To Name (manager's name)

To see an example, download the [example input data]. 

### What are system requirements? ###
You need Microsoft PowerPoint 16.* and Microsoft Excel 16.*

**MyBoss** was manually tested under:
- PC: Microsoft PowerPoint 2016 MSO (16.0.9126.2259) 32-bit + Microsoft Excel 2016 MSO (16.0.9126.2259) 32-bit
- Mac: Microsoft PowerPoint for Mac Version 16.15 (180709) + Microsoft Excel for Mac Version 16.15 (180709)

### How to run MyBoss on Mac? ###
Same as with Windows, you need to [download the tool](https://github.com/devrazdev/MyBoss/raw/master/MyBoss.pptm) and open the file.

*NB: When you open the file, security warning may come up. It usually happens because PowerPoint restricts running VBA code without user consent, while **MyBoss** is a 100% VBA solution. So, if such a security warning comes up, just click "Enable content".*

However, there is one more step ahead.

Due to the file access restrictions  ([reading Excel files from PowerPoint require AppleScript]), you will need to put [this AppleScript file] to this folder:
```bash
~/Library/Application Scripts/com.microsoft.Powerpoint/
```
before running the **MyBoss**. 
*NB: Do not change the name of this file since it's hardcoded in MyBoss!*
*NB2: If you then open [MyBoss](https://github.com/devrazdev/MyBoss/raw/master/MyBoss.pptm) file and see empty OrgChart tab, this means it requires resolving security issues*
1. *Go to PowerPoint -> Preferences -> Security*
2. *Click "Enable all macros"*
3. *Click "Trust access to the VBA project object model"*
4. *Allow actions to run programs without notification*
5. *Reopen the file*

To perform a test run:
1. Open [MyBoss](https://github.com/devrazdev/MyBoss/raw/master/MyBoss.pptm)
2. Go to "Org chart" tab
3. Click "Open"
4. Select [example input data]
5. Select the spreadsheet you like
6. Click "Upload"
7. Once loaded, click "Create org chart" -> "Single slide org structure"
8. Wait until it finishes

[this AppleScript file]: <https://github.com/devrazdev/MyBoss/raw/master/misc/MyBoss-browse_files_on_mac.scpt>
[reading Excel files from PowerPoint require AppleScript]: <https://developer.microsoft.com/en-us/office/blogs/VBA-improvements-in-Office-2016/>

---

## Developer's corner ##
### What is the technology behind MyBoss? ###
Technically, **MyBoss** is a VBA solution — PowerPoint file with macros and a custom tab. 

### Are there any hidden dependencies? ###
The only third-party module used is Tim Hall's custom implementation of Dictionary class  to support Mac ([available on github]). Thanks, Tim.

[available on github]: <https://github.com/VBA-tools/VBA-Dictionary>

### Why did you choose to make a VBA solution? ###
There are 3 ways to build custom solutions for Office suite:
1. VBA solution
2. Visual Studio Tools for Office (VSTO) Add-in
3. JavaScript API Add-in

Their comparison is presented [here] and [there]. Basically, Office for Mac doesn't support VSTO Add-ins and JavaScript API for PowerPoint is yet too limited (July'18).

[here]: <https://docs.microsoft.com/en-us/visualstudio/vsto/vba-and-office-solutions-in-visual-studio-compared>
[there]: <https://docs.microsoft.com/en-us/office/dev/add-ins/overview/office-add-ins#StartBuildingApps_TypesofApps>

### How to customize MyBoss on my own? ###
1. To customize core, you will have to use Office Visual Basic Editor, since VBA code is stored inside the *MyBoss.pptm* file in binary format.
    - PC: type Alt+F11 or go to "Developer" tab -> Visual Basic;
    - Mac: go to Tools -> Macro -> Visual Basic Editor.
2. To customize UI tab (Ribbon XML):
[Reference guide on UI], [Mac Ribbon examples], [Win Ribbon examples]
    - PC: Suggest using utility [OfficeCustomUIEditorSetup] (requires [.NET 3.0](https://www.microsoft.com/en-us/p/surface-laptop-3/8VFGGH1R94TM))
    - Mac: Suggest you find a PC. [However], if you change the extension of *MyBoss.pptm* from PPTM to ZIP and look inside the archive, you will find the Ribbon XML, which then you can edit (folder "customUI")
3. To customize the design of organizational charts:
    - PC & Mac: edit the Templates on slide 1, preserving their names and their grouping. [Learn how to check the names of shapes using Selection pane]

[Reference guide on UI]: <https://msdn.microsoft.com/en-us/library/dd926139(v=office.12).aspx>
[Mac Ribbon examples]: <https://www.rondebruin.nl/mac/macfiles/MacRibbonExamples.dmg>
[Win Ribbon examples]: <https://www.rondebruin.nl/win/winfiles/RibbonExampleFiles.zip>
[OfficeCustomUIEditorSetup]: http://www.rondebruin.nl/win/winfiles/OfficeCustomUIEditorSetup.zip
[However]: <https://support.office.com/en-us/article/extract-files-or-objects-from-a-powerpoint-file-85511e6f-9e76-41ad-8424-eab8a5bbc517>
[Learn how to check the names of shapes using Selection pane]:<https://support.office.com/en-us/article/manage-objects-with-the-selection-pane-a6b2fd3e-d769-46c1-9b9c-b94e04a72550>

## Farewell ##
I would be happy to hear any feedback about your use of **MyBoss**. Feel free to write me at nikitobot@gmail.com. Thank you.

## Thanks to contributors ❤️
- **Anna Glushkova** — for keeping an eagle eye on technical part and being a devoted user
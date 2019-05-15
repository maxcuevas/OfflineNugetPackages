# OfflineNugetPackages

Go to this link for how to get offline nuget packages to work: https://blogs.msdn.microsoft.com/joetalksmicrosoft/2017/08/14/offline-nuget-packages-with-vs-net-2017/

Text copied from link just in case it goes down. 

So, I work with a customer that has thier development network offline of the general internet.
One of the development leads built a template for VS.NET (2015) which has all the NuGet packages.
Well, I am running VS.NET 2017, yes I like to run the latest and greatest!
First off, I created a new solution with the template. I then built the solution and had a large number of references to dll's missing.
After a review of the NuGet manager I found that many of the packages said hey were not avaiable in the source. Yet they were listed in the installed section of the manager.
I went about changing things but I did it out of order so here we will do it in order:
First you msut add the location of the new packages (note, the template should probably have installed them correctly but for vairous reasons it didn't):
The following is generic:
To manage package sources: 
Select the Settings icon in the Package Manager UI outlined below or use the Tools > Options command and scroll to NuGet Package Manager: 

Select the Package Sources node: 

To add a source, select +, edit the name, enter the URL or path in the Source control, and select Update. The source now appears in the selector drop-down.
To change a package source, select it, make edits in the Name and Source boxes, and select Update.
To disable a package source, clear the box to the left of the name in the list.
To remove a package source, select it and then select the X button.
Use the up and down arrow buttons to change the priority order of the package sources. Visual Studio searches these sources in the priority order when restoring packages for a project.
What needs to be done is as follows:
Uncheck the "nuget.org" as all you get is erors because you can't reach it.
Add a new source as the instructions state above. The source would be where the packages are located. In my case I did a search for the template name, then I went one folder back, then clicked on "packages" and all the packages where there. This is the path of the packages that were embeded in the template.
Once you have the source then you are ready for the next step (while the solution with the missing assemblies is open):
Go to: Tools->NuGet Package Manager->Package Manager Console
This opens a console window to run powershell.
Run the following:
Update-Package -reinstall
Now do a rebuild of the solution and all of the references will be resolved.
Note: Once this is done one time on the machine in question, anytime you use the same template again you will not run into this issue.

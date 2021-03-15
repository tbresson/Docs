# How to setup your .NET Core project with Xunit

"ProjectName" could be anything you like.

* Enter the folder where you keep all of your projects
* Create a folder with the ProjectName and enter it
* dotnet new console -o ProjectName
* dotnet new xunit -o ProjectName.Test
* dotnet add ProjectName.Test/ProjectName.Test.csproj reference ProjectName/ProjectName.csproj

You can now build your project if you're in the ProjectName folder and Test your project if you're in the ProjectName.Test folder.
You can also add both projects to a solution so you can build all projects at the same time (and also add intellisense to VSCode):

* dotnet new sln
* dotnet sln add ProjectName/ProjectName.csproj
* dotnet sln add ProjectName.Test/ProjectName.Test.csproj

Test it works:

* dotnet build (from the ProjectName folder where both projects are (and the solution file))
* dotnet test

To run it you need to add the --project parameter:

* dotnet run --project ProjectName/ProjectName.csproj

or you can be in the project directory and run the test with a reference to the test project (or solution file) as a parameter:

* dotnet test '../ProjectName.Test/ProjectName.Test.csproj'

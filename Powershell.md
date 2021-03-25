# Powershell

## Help

Get-Help or Help
Get-Help <something> -Full          # Show the complete help information
Get-Help <something> -Online        # Show the online version of the help
Get-Help <something> -ShowWindow    # Show the help in a external Window
Update-Help -Force

## Helpful

Get-Module -ListAvailable           # Show the available module that can be imported
<cmdlet> | Get-Member (or gm)       # Show the cmdlet's properties, methods etc.


## Define

$variableName                       # Define a variable
@{}                                 # Define a hash table
$_                                  # The current object from the pipeline, e.g. Get-Service | Where-Object {$_.Name -like 'B'}

## Parameters

-Filter                             # Filters (limits) the return result (used before Where-Object)
-Select-Object                      # Selects an object from the pipeline
-Where-Object                       # Filters the return result after getting the result, e.g. Where-Object Name -eq "BITS"
-Sort-Object                        # Sorts the object(s) from the pipeline in the order specified, Sort-Object Name, Status
-ExpandProperty                     # Selects the value of the property instead of the property (as an object)
-ScriptBlock                        # Creates a block of code that can be used as a single unit, e.g. Invoke-Command -ScriptBlock { Get-Process }

## Operators

-eq                                 # Equal
-ne                                 # Not equal
-gt                                 # Greater than
-lt                                 # Less than
-and
-or
&                                   # Call operator, e.g. $a = "Get-ExecutionPolicy"; & $a (run the content of the variable)

## Output

-Format-Table (or -FT)              # Formats the output in table form (Excel like)
-AutoSize                           # Used with -FT to prevent truncating columns (except if there are no room at the end of the screen)
-Format-List (or -FL)               # Formats the output in a list (line by line; used if many properties are listed)
-Out-GridView                        # Used after a pipeline to output the result in a grid Window

## Run / Execute

Invoke-Expression                   # Run an expression, e.g. Invoke-Expression -Command "1+1"
Invoke-Command                      # Run a command locally or remote, e.g. Invoke-Command -ScriptBlock {notepad.exe}

## Debug

-WhatIf                             # Shows a descriptive text about what will happen if run
-Confirm                            # Requires a confirmation before completing the action

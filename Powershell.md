# Powershell

## Help

    Get-Help or Help
    Get-Help something -Full        # Show the complete help information
    Get-Help something -Online      # Show the online version of the help
    Get-Help something -ShowWindow  # Show the help in a external Window
    Update-Help -Force

## Helpful

    Get-Command -Name X             # Show all the commands that are available on your system
    Get-Module -ListAvailable       # Show the available module that can be imported
    cmdlet | Get-Member (or gm)     # Show the cmdlet's properties, methods etc.
    | more                          # Prevents text from scrolling off page/screen

## Define

    $variableName                   # Define a variable
    $using:variableName             # Uses the variable defined outside scope, e.g. with Invoke-Command
    @{}                             # Define a hash table (key-value pair)
    @()                             # Define an array
    $_                              # The current object from the pipeline, e.g. Get-Service | Where-Object {$_.Name -like 'B'}

## Parameters

    -Filter                         # Filters (limits) the return result (used before Where-Object)
    -Select-Object                  # Selects an object from the pipeline (or ues * to select ALL properties/values)
    -First X                        # Used with Select-Object to get the first X results, e.g. -First 1
    -Unique                         # Returns all the unique values, e.g. Get-Service | Select-Object Status -Unique could return: Stopped and Running
    -Where-Object                   # Filters the return result after getting the result, e.g. Where-Object Name -eq "BITS"
    -Sort-Object                    # Sorts the object(s) from the pipeline in the order specified, Sort-Object Name, Status
    -ExpandProperty                 # Selects the value of the property instead of the property (as an object)
    -ScriptBlock                    # Creates a block of code that can be used as a single unit, e.g. Invoke-Command -ScriptBlock { Get-Process }
    -Split X                        # Returns each value from a separated list, e.g. $env:psmodulepath -Split ";"

## Operators

    -eq                             # Equal
    -ne                             # Not equal
    -gt                             # Greater than
    -lt                             # Less than
    -like
    -contains
    -and
    -or
    &                               # Call operator, e.g. $a = "Get-ExecutionPolicy"; & $a (run the content of the variable)

## Properties

    Custom property                 # E.g. Get-Process | select Name, @{Name='Runtime';Expression={(Get-Date) - $_.StartTime}}
    -ExpandProperty                 # If the property contains a nested object, an array of objects or you simply want the value

## CIM - Common Information Model

    Get-CimClass                    # E.g. Get-CimClass -ClassName Win32_OperatingSystem
    Get-CimInstance                 # E.g. Get-CimInstance -ClassName Win32_BIOS | Select Manufacturer, SerialNumber
    New-CimSession                  # E.g. New-CimSession -Computername srv1 -credential company\administrator

## Output

    -Format-List (or -FL)           # Formats the output in a list (line by line; used if many properties are listed)
    -Format-Table (or -FT)          # Formats the output in table form (Excel like)
    -AutoSize                       # Used with -FT to prevent truncating columns (except if there are no room at the end of the screen)   
    -Format-Wide                    # 
    -Out-GridView                   # Used after a pipeline to output the result in a grid Window

## File output

    -Out-File fileName.txt          # -NoClubber (won't overwrite existing file), -Append (append to an existing file)
    -Export-CSV fileName.csv

## Run / Execute

    Invoke-Expression               # Run an expression, e.g. Invoke-Expression -Command "1+1"
    Invoke-Command                  # Run a command locally or remote, e.g. Invoke-Command -ScriptBlock {notepad.exe}

## Debug

    -WhatIf                         # Shows a descriptive text about what will happen if run
    -Confirm                        # Requires a confirmation before completing the action

## Remote

    New-CimSession                  # Create a remote session, e.g. $CS = New-CimSession -ComputerName $ComputerName -Credential $cred
                                    # Example of use: Get-DNSClientServerAddress -CimSession $CS
    New-PSSession                   # Create a remote Powershell session and enter it, e.g. New-PSSession -$ComputerName Srv1 -Credential $cred

## Loops

    $services = Get-Service         # ForEach doesn't add anything to the pipeline
    ForEach ($s in $services) {   
        $status = $s.Status

        if ($status -eq 'Running') {
            write-host "$($s.Name) running"
        }
    }

## Functions

    Function Print-String {         # Basic function
        Param(
            [string]$String
        )
        Write-Output $String
    }

    Function Print-String {         # Advanced function
        [CmdletBinding()]
        Param(
            [string]$String
        )
        Write-Output $String
    } 

    Function Print-String {         # Mandatory/required parameter
        [CmdletBinding()]
        Param(
            [Parameter(Mandatory)]
            [string]$String
        )
        Write-Output $String
    }

    Function Print-String {         # Default parameter value
        [CmdletBinding()]           # Parameters with default values cannot be optional
        Param(
            [Parameter()]
            [string]$String = "Hello world"
        )
    }    

## Function validation

    Function Print-TopThree {       # ValidateCount(1,3) says there can only be 1, 2 or 3 values for the parameter TopThree
        [CmdletBinding()]           # Notice the string[] is an array 
        Param(
            [Parameter()]
            [ValidateCount(1,3)]
            [string[]]$TopThree
        )
    }

    Function Get-Folder {           # ValidateScript must return true for the scrip to run (path must exist)
        [CmdletBinding()]           
        Param(                      
            [Parameter()]
            [ValidateScript({
                Test-Path -Path $_ -PathType Container
            })]            
            [string]$Path
        )
    }

    Function Get-Folder {           # ValidatePattern must match (path must be on c-drive)
        [CmdletBinding()]           # Test like this: 'C:\foldername' -match '^C:\\'
        Param(                      
            [Parameter()]
            [ValidatePattern("^C:\\")]
            [string]$Path
        )
    }

    Function Get-It {               # ValidateSet means the variable can only be what's pre-defined.
        [CmdletBinding()]
        Param(
            [Parameter()]
            [ValidateSet("Yes", "No")]
            [string]$Really
        )
    }

    Function Set-MemoryInMB {       # ValidateRange means the parameter value must between 512 and 4096
        [CmdletBinding()]
        Param(
            [Parameter()]
            [ValidateRange(512, 4096)]
            [int]$MemoryInMB
        )
    }

    Function Get-Something {        # ValidateNotNullOrEmpty, ValidateNotNull, AllowNull 
        [CmdletBinding()]           # ValidateNotNull doesn't work if you specify a type, e.g. string       
        Param(
            [Parameter()]
            [ValidateNotNullOrEmpty()]
            [string]$Name,
            
            [Parameter()]
            [ValidateNotNull()]
            $LastName,
            
            [Parameter()]
            [AllowNull()]
            [string]$FriendlyName
        )
    }    

    Function Get-Something {        # Call this function with either Name or Id (same set) or nothing at all which defaults to the None set
        [CmdletBinding(DefaultParameterSetName = "None")]
        Param(
            [Parameter(Mandatory, ParameterSetName = 'ByName')]
            [string]$Name,
            
            [Parameter(Mandatory, ParameterSetName = 'ById')]
            [int]$Id
        )
    }

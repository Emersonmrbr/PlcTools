---
external help file: Format-RssToAcd-help-en-US.xml
Module Name: Format-RssToAcd
online version:
schema: 2.0.0
---

# Format-RssToAcd

## SYNOPSIS

Converts RSS (Rockwell Software) format files to ACD (Allen-Bradley ControlLogix project) format using customizable regular expression mappings.

## SYNTAX

```
Format-RssToAcd [-Path] <String> [-Backup] [-Extension] <string> [-RegexMapPath <string>] [-Quiet] [-ProgressAction <ActionPreference>] [<CommonParameters>]
```

## DESCRIPTION

The Format-RssToAcd module provides a function to automate the conversion of files from the RSS format to the ACD format, commonly used in PLC migration or integration scenarios. The function reads a set of regular expression patterns and replacements from a JSON file (`RegexMap.json`) and applies them to the target file(s). Optional backup creation is supported before making changes. This tool is useful for engineers and developers working with industrial automation projects who need to modernize or migrate legacy PLC programs.

> [!NOTE]
> The `RegexMap.json` file must be present in the same directory as the module, unless a custom path is specified with `-RegexMapPath`. Each entry in the JSON must contain both `Pattern` and `Replacement` properties.

## EXAMPLES

### Example 1

```powershell
PS C:\> Format-RssToAcd -Path "C:\Temp\PlcFiles.xml"
```

This example formats the file `PlcFiles.xml`, changes the format variable from .rss to .acd, uses the RegexMap.json with the base configuration, and does not create a backup. This function will convert formats like "{::[LinkName]B3:0/0}" to "{::[LinkName]B3[0].0}".

### Example 2

```powershell
PS C:\> Format-RssToAcd -Path "C:\Temp\PlcFiles.xml" -Backup
```

This example formats the file `PlcFiles.xml`, changes the format variable from .rss to .acd, uses the RegexMap.json with the base configuration, and creates a backup. This function will convert formats like "{::[LinkName]B3:0/0}" to "{::[LinkName]B3[0].0}".

### Example 3

```powershell
PS C:\> Format-RssToAcd -Path "C:\Temp\PlcFiles" -Extension "*.xml"
```

This example processes all `.xml` files in the `C:\Temp\PlcFiles` directory, applies the regex replacements defined in RegexMap.json, and does not create backups. This is useful when you need to convert multiple files with a specific extension other than `.xml`.

### Example 4

```powershell
PS C:\> Format-RssToAcd -Path "C:\Temp\PlcFiles" -Extension "*.txt"
```

This example processes all `.txt` files in the `C:\Temp\PlcFiles` directory, applies the regex replacements defined in RegexMap.json, and does not create backups. This is useful when you need to convert multiple files with a specific extension other than `.xml`.

### Example 5

```powershell
PS C:\> Format-RssToAcd -Path "C:\Temp\PlcFiles" -Extension "*.csv" -Backup
```

This example processes all `.csv` files in the `C:\Temp\PlcFiles` directory, creates a backup for each file, and applies the regex replacements defined in RegexMap.json.

### Example 6

```powershell
PS C:\> Format-RssToAcd -Path "C:\Temp\PlcFiles" -RegexMapPath "C:\Custom\RegexMap.json" -Quiet
```

This example processes all `.xml` files in the `C:\Temp\PlcFiles` directory using a custom regex map file and suppresses output to the host, returning only the result object.

## PARAMETERS

### -Path

The full path to the file to be modified, or to a directory containing files to process.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Extension

The file extension filter to use when searching for files in a directory. Default is `*.xml`. Ignored if `-Path` is a file.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: *.xml
Accept pipeline input: False
Accept wildcard characters: False
```

### -Backup

Creates a backup of the original file with a .bak extension before making any changes.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -RegexMapPath

(Optional) The full path to a custom RegexMap.json file. If not specified, uses the default in the module directory.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Quiet

Suppresses output to the host. Only returns the result object.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ProgressAction

Determines how PowerShell responds to progress updates generated by a script, cmdlet, or provider, such as the progress bars generated by the Write-Progress cmdlet. The Write-Progress cmdlet creates progress bars that show a command's status. The ProgressAction parameter was added in PowerShell 7.4.

```yaml
Type: ActionPreference
Parameter Sets: (All)
Aliases: proga

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### None

## OUTPUTS

### Object[]

Returns an array of objects with details about each file processed, including file path, whether it was changed, which regex patterns were applied, and any error message if processing failed.

## NOTES

## RELATED LINKS
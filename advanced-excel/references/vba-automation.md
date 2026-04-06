# VBA Automation

Patterns and techniques for automating Excel workflows using Visual Basic for Applications (VBA).

---

## Module Structure and Best Practices

Organize VBA projects with a clear module structure:

| Module Type | Naming Convention | Purpose |
|-------------|-------------------|---------|
| Standard Module | `mod_` prefix | Utility functions, main procedures |
| Class Module | `cls_` prefix | Object-oriented patterns, custom objects |
| UserForm | `frm_` prefix | Dialog boxes, input forms |
| ThisWorkbook | (built-in) | Workbook-level events |
| Sheet Modules | (built-in) | Sheet-level events |

Always include `Option Explicit` at the top of every module to enforce variable declaration and catch typos at compile time.

## Common Automation Patterns

### Report Generation

```vba
Sub GenerateMonthlyReport()
    Dim wsData As Worksheet, wsReport As Worksheet
    Dim lastRow As Long
    
    Application.ScreenUpdating = False
    Application.Calculation = xlCalculationManual
    
    Set wsData = ThisWorkbook.Sheets("RawData")
    Set wsReport = ThisWorkbook.Sheets("Report")
    
    lastRow = wsData.Cells(wsData.Rows.Count, "A").End(xlUp).Row
    
    ' Clear previous report
    wsReport.UsedRange.ClearContents
    
    ' Copy headers
    wsData.Range("A1:F1").Copy wsReport.Range("A1")
    
    ' Filter and copy relevant data
    wsData.Range("A1:F" & lastRow).AutoFilter Field:=3, Criteria1:=Format(Date, "MMMM")
    wsData.Range("A2:F" & lastRow).SpecialCells(xlCellTypeVisible).Copy wsReport.Range("A2")
    wsData.AutoFilterMode = False
    
    ' Format report
    With wsReport.Range("A1:F1")
        .Font.Bold = True
        .Interior.Color = RGB(0, 70, 130)
        .Font.Color = vbWhite
    End With
    
    wsReport.Columns("A:F").AutoFit
    
    Application.Calculation = xlCalculationAutomatic
    Application.ScreenUpdating = True
    
    MsgBox "Report generated successfully.", vbInformation
End Sub
```

### Email Automation with Outlook

```vba
Sub SendReportEmail(recipient As String, subject As String, filePath As String)
    Dim olApp As Object, olMail As Object
    
    Set olApp = CreateObject("Outlook.Application")
    Set olMail = olApp.CreateItem(0)
    
    With olMail
        .To = recipient
        .Subject = subject
        .Body = "Please find the attached report for " & Format(Date, "MMMM YYYY") & "."
        .Attachments.Add filePath
        .Send
    End With
    
    Set olMail = Nothing
    Set olApp = Nothing
End Sub
```

### Batch File Processing

```vba
Sub ProcessAllFilesInFolder()
    Dim folderPath As String, fileName As String
    Dim wb As Workbook
    
    folderPath = "C:\Reports\Incoming\"
    fileName = Dir(folderPath & "*.xlsx")
    
    Do While fileName <> ""
        Set wb = Workbooks.Open(folderPath & fileName)
        ' Process each workbook
        Call ProcessWorkbook(wb)
        wb.Close SaveChanges:=True
        fileName = Dir()
    Loop
End Sub
```

## Error Handling Framework

```vba
Sub RobustProcedure()
    On Error GoTo ErrorHandler
    
    ' Main logic here
    
    Exit Sub

ErrorHandler:
    Dim errMsg As String
    errMsg = "Error " & Err.Number & ": " & Err.Description & vbCrLf & _
             "Source: " & Err.Source
    
    ' Log to error sheet
    Call LogError(errMsg)
    
    MsgBox errMsg, vbCritical, "Error Occurred"
    
    ' Clean up
    Application.ScreenUpdating = True
    Application.Calculation = xlCalculationAutomatic
End Sub
```

## Performance Optimization

- **Disable screen updating**: `Application.ScreenUpdating = False` before loops, re-enable after.
- **Manual calculation**: Switch to `xlCalculationManual` during data writes, restore after.
- **Avoid Select/Activate**: Reference ranges directly (`ws.Range("A1").Value = x`) instead of selecting first.
- **Use arrays for bulk operations**: Read ranges into arrays, process in memory, write back in one operation.
- **Minimize interactions with the sheet**: Each read/write to a cell is slow — batch operations with `Range.Value = Array`.

# Power Query Advanced Techniques

Advanced data transformation patterns using Power Query (M language) in Excel and Power BI.

---

## Custom Functions

Create reusable transformation logic by defining custom functions in Power Query. Use these for repetitive operations across multiple queries or tables.

### Parameter-Based Function

```m
(FilePath as text, SheetName as text) =>
let
    Source = Excel.Workbook(File.Contents(FilePath), null, true),
    Sheet = Source{[Item=SheetName, Kind="Sheet"]}[Data],
    Promoted = Table.PromoteHeaders(Sheet, [PromoteAllScalars=true]),
    Typed = Table.TransformColumnTypes(Promoted, {{"Date", type date}, {"Amount", type number}})
in
    Typed
```

Invoke this function from other queries or use it with `Table.AddColumn` to process a list of files dynamically.

### Folder-Based Import Pattern

Combine all files from a folder with consistent schemas:

```m
let
    Source = Folder.Files("C:\Data\Monthly"),
    Filtered = Table.SelectRows(Source, each [Extension] = ".xlsx"),
    AddContent = Table.AddColumn(Filtered, "Tables", each Excel.Workbook([Content])),
    Expanded = Table.ExpandTableColumn(AddContent, "Tables", {"Data", "Item"}),
    FilterSheets = Table.SelectRows(Expanded, each [Item] = "Summary"),
    Combined = Table.Combine(FilterSheets[Data])
in
    Combined
```

## Advanced Transformations

### Unpivot and Pivot Patterns

Transform wide tables to tall format for analysis:

```m
// Unpivot month columns to rows
Table.UnpivotOtherColumns(Source, {"Product", "Region"}, "Month", "Revenue")
```

Reverse the operation with:
```m
Table.Pivot(Source, List.Distinct(Source[Month]), "Month", "Revenue", List.Sum)
```

### Conditional Column Logic

Build complex conditional columns using nested `if` or `Table.AddColumn` with custom logic:

```m
Table.AddColumn(Source, "Tier", each
    if [Revenue] >= 1000000 then "Enterprise"
    else if [Revenue] >= 100000 then "Mid-Market"
    else if [Revenue] >= 10000 then "SMB"
    else "Micro"
, type text)
```

### Grouped Aggregations

```m
Table.Group(Source, {"Region"}, {
    {"TotalRevenue", each List.Sum([Revenue]), type number},
    {"AvgDealSize", each List.Average([DealSize]), type number},
    {"Count", each Table.RowCount(_), Int64.Type},
    {"MaxDate", each List.Max([CloseDate]), type date}
})
```

## Error Handling

Wrap transformations with error handling to prevent query failures on dirty data:

```m
Table.AddColumn(Source, "SafeAmount", each try Number.From([RawAmount]) otherwise 0, type number)
```

For row-level error capture:
```m
Table.AddColumn(Source, "ParseResult", each try [Expression] catch (e) => e[Message])
```

## Performance Tips

| Technique | Description |
|-----------|-------------|
| **Query folding** | Keep transformations foldable (push to source) by avoiding custom M functions early in the pipeline |
| **Buffer tables** | Use `Table.Buffer` for tables referenced multiple times to avoid re-evaluation |
| **Remove unnecessary columns** | Drop columns early with `Table.SelectColumns` to reduce memory |
| **Disable load** | Set intermediate helper queries to not load into the data model |
| **Native queries** | Use `Value.NativeQuery` for SQL sources to push complex logic to the database |

Check query folding status by right-clicking a step — if "View Native Query" is available, folding is active.

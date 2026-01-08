# Log Parsers

KQL functions to normalize raw `SecurityEvent` logs into structured fields for easier querying and detection rule writing.

## Why Parsers? 

Sysmon and PowerShell logs arrive in `SecurityEvent` table with data stored as XML in the `EventData` field. Parsing XML in every query is: 
- Repetitive
- Error-prone
- Hard to read

These parsers extract fields once, so your detection queries stay clean.

## Available Parsers

| Parser | Function Name | Log Source |
|--------|---------------|------------|
| Sysmon | `SysmonParsed` | Microsoft-Windows-Sysmon/Operational |
| PowerShell | `PowerShellParsed` | Microsoft-Windows-PowerShell/Operational |

## How to Deploy

### Step 1: Open Sentinel Logs

Go to **Sentinel > Logs**

### Step 2: Create Sysmon Function

1. Copy the contents of `Sysmon-Operational-Parser.txt`
2. Paste into the query editor
3. Click **Save > Save as function**
4. Configure:
   | Field | Value |
   |-------|-------|
   | Function name | `SysmonParsed` |
   | Legacy category | `Custom` |
5. Click **Save**

<p align="center">
  <img width="700" height="450" alt="SysmonParsed"
       src="https://github.com/user-attachments/assets/dcd53613-9529-40b8-aa3f-7266b026cd8c">
</p>
<p align="center"><em>Figure: SysmonParsed</em></p>

### Step 3: Create PowerShell Function

1. Copy the contents of `PowerShell-Operational-Parser.txt`
2. Paste into the query editor
3. Click **Save > Save as function**
4. Configure:
   | Field | Value |
   |-------|-------|
   | Function name | `PowerShellParsed` |
   | Legacy category | `Custom` |
5. Click **Save**

<p align="center">
  <img width="700" height="450" alt="PowerShellParsed"
       src="https://github.com/user-attachments/assets/568a8197-8aa4-4d38-9574-2d9beb24ccc7">
</p>
<p align="center"><em>Figure: PowerShellParsed</em></p>

### Step 4: Verify

Wait 1-2 minutes, then test:

```kql
SysmonParsed
| take 10
```

<p align="center">
  <img width="700" height="450" alt="SysmonParsed"
       src="https://github.com/user-attachments/assets/15eac61f-0c16-4d9f-b11d-0e3cee3cf19b">
</p>
<p align="center"><em>Figure: Query Results</em></p>

## Reference

Parsers based on: 
- [Azure-Sentinel Sysmon-AllVersions Parser](https://github.com/Azure/Azure-Sentinel/blob/master/Parsers/Sysmon/Sysmon-AllVersions_Parser.txt)
- [Improved Sysmon Sentinel Kusto Parser](https://gist.github.com/fryguy04/0d673f64c386df7903e175b11cfe31e5)

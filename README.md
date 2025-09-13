# Invoke-ShareHunterX

Invoke-ShareHunterX is a modified version of Invoke-ShareHunter, originally developed by Leo4j, with additional features beyond enumerating the domain for readable and writable shares:
- Enumerates interesting files in readable shares that may contain credentials or secrets
- Generates output in CSV format

## Usage

### Basic Share Enumeration

```powershell
Invoke-ShareHunterX
Invoke-ShareHunterX -Domain yourdomain.local
Invoke-ShareHunterX -Targets "host1,host2"
Invoke-ShareHunterX -TargetsFile C:\path\to\targets.txt
```

### Searching for Files by Pattern

To search for files by pattern, provide a file containing filename patterns (see `patterns.txt` for examples):

```powershell
Invoke-ShareHunterX -PatternsFile C:\path\to\patterns.txt
```

#### Adding Custom Filename Patterns

Use the asterisk (*) wildcard to specify all files with the `.config` extension:

```sh
*.config
```

Other examples:

```sh
abc.txt      # file named 'abc.txt'
credit*      # file names starting with 'credit'
*secret*     # file names containing 'secret'
```

### Verbose Output

Add the `-Verbose` parameter to instantly display the list of files found in the PowerShell prompt.

```powershell
PS C:\Users\tester\Desktop\Invoke-ShareHunterX> Invoke-ShareHunterX -PatternsFile .\patterns.txt -Verbose

[+] Enumerating Computer Objects...
[+] Running Port Scan...
[+] Enumerating Shares...
[+] Testing Read Access...
...

[+] Output saved to: C:\Users\tester\Desktop\Invoke-ShareHunterX\Shares_Results.txt and C:\Users\tester\Desktop\Invoke-ShareHunterX\Shares_Results.csv

...
[+] Searching for files matching patterns in readable shares
[*] Patterns used: *.exe, *.msi, *.txt
[+] Files found in readable shares matching patterns:

FullName                                                         Length  CreationTime         LastWriteTime        Domain
--------                                                         ------  ------------         -------------        -----
\\server21.abc.com\Shared\User\installer.msi                       53373 5/13/2025 8:07:08 PM 8/2/2025 8:07:08 PM  ab...
\\pc2.abc.com\Shared\dasda.txt                                     12    6/13/2025 2:55:19 PM 7/2/2025 2:55:19 PM  ab...

[+] Output saved to: C:\Users\tester\Desktop\Invoke-ShareHunterX\Files_Results.txt and C:\Users\tester\Desktop\Invoke-ShareHunterX\Files_Results.csv
```

## Credits

- Invoke-ShareHunter by Leo4j (https://github.com/Leo4j/Invoke-ShareHunter)
- File name pattern sample from PowerHuntShares by NetSPI (https://github.com/NetSPI/PowerHuntShares/)
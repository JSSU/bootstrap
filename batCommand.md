 IE --> Tools--> Internet Options
 								 --> Security --> Custom Level --> Scroll down to look for option called " Display Mixed Content"
 IE --> Tools -->Internet Options
 								 --> Security --> Local intranet --> Sites --> Advanced --> "Add this website to the zone: " --> Add
Batch create log file when login
```Batch
echo %USERNAME% logged on at %DATE% %TIME% >> log.txt

```

Change windows IE options
```Batch
@Echo off&title gworks
set "a=HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\ZoneMap\Domains\"
set b=192.168.1.100
reg add "%a%%b%" /v http /t REG_DWORD /d 2 /f >nul 2>nul
reg add "%a%%b%" /v https /t REG_DWORD /d 2 /f >nul 2>nul

```
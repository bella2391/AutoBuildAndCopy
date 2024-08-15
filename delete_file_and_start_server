@echo off
chcp 65001
setlocal

rem directory structure like /path/to/project/build/libs/sample.jar
rem variebles set
set "flag=false"
set "dirA=/path/to/minecraft/server/mods"
set "fileB=sample.jar"
set "dirB=/path/to/build/libs"
set "otherBatFile=/path/to/other.bat"
set "dirG=/path/to/project"

rem execute `.\gradlew build` in directory G
cd /d "%dirG%"
call java17.bat
call .\gradlew build
if %errorlevel% neq 0 (
    echo Suspended processing by fail of gradlew build in %dirG%.
    exit /b %errorlevel%
)

cd /d "%~dp0%"  rem back the first directory
rem check existence of fileB in directoryA, if exists, delete it
if exist "%dirA%\%fileB%" (
    del "%dirA%\%fileB%" 2>nul
    if exist "%dirA%\%fileB%" (
        echo %fileB% is locked.
    ) else (
        echo Deleted %fileB%.
        set "flag=true"
    )
) else (
    echo %fileB% does not exist in %dirA%.
    set "flag=true"
)

if "%flag%"=="true" (
    echo Flag is true, so processing
    rem check existence of fileB in directoryB, if exists, delete it
    if exist "%dirB%\%fileB%" (
        copy "%dirB%\%fileB%" "%dirA%\"
        echo Copied %fileB% into %dirA%
        if "%otherBatFile%"=="" (
            echo Bat file will not call by empty of otherBatFile.
        ) else (
            echo Call bat file: %otherBatFile%
            call "%otherBatFile%"
        )
    ) else (
        echo %fileB% does not exist in %dirB%.
    )
) else (
    echo Flag is false, so Suspended processing
)

endlocal

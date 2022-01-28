FROM mcr.microsoft.com/windows/servercore:ltsc2019

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop';$ProgressPreference='silentlyContinue';"]

ARG RUNNER_VERSION=2.287.1

RUN Invoke-WebRequest -Uri 'https://aka.ms/install-powershell.ps1' -OutFile install-powershell.ps1; ./install-powershell.ps1 -AddToPath; Invoke-WebRequest -Uri https://github.com/actions/runner/releases/download/v$env:RUNNER_VERSION/actions-runner-win-x64-$env:RUNNER_VERSION.zip -OutFile runner.zip; Expand-Archive -Path C:/runner.zip -DestinationPath C:/actions-runner

RUN iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
RUN choco install -y git
RUN setx /M PATH $($Env:PATH + ';C:\Program Files\Git\bin')

ADD runner.ps1 C:/runner.ps1
CMD ["powershell", ".\\runner.ps1"]

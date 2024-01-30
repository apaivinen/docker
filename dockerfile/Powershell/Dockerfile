# Use an official Python runtime as a parent image
FROM mcr.microsoft.com/powershell

# Install AzCLI
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash

# Install latest AZ module from powershell gallery
RUN pwsh -Command \
    Install-Module -Name az -Repository PSGallery -Force

# Install latest Microsoft.Graph module from powershell gallery
RUN pwsh -Command \
    Install-Module -Name Microsoft.Graph -Repository PSGallery -Force

# Install latest PnP.Powershell module from powershell gallery
# You can specify powershell version by using parameter: -RequiredVersion
# Here you can find PnP.Powershell versions: https://github.com/pnp/powershell/releases
RUN pwsh -Command \
    Install-Module -Name PnP.Powershell -Repository PSGallery -Force

# Install Terminal Icons
RUN pwsh -Command \
    Install-Module -Name Terminal-Icons -Repository PSGallery -Force

# Install oh-my-posh
RUN pwsh -Command \
    Install-Module -Name oh-my-posh -Repository PSGallery -Force

# Install PSReadLine
RUN pwsh -Command \
    Install-Module -Name PSReadLine -Repository PSGallery -Force

#Copy oh-my-posh-profile.json
COPY oh-my-posh-profile.json /root/.config/powershell/oh-my-posh-profile.json

# Profile
# /root/.config/powershell/Microsoft.PowerShell_profile.ps1
RUN echo "Import-Module -Name Terminal-Icons" >> /root/.config/powershell/Microsoft.PowerShell_profile.ps1
RUN echo "import-module psreadline" >> /root/.config/powershell/Microsoft.PowerShell_profile.ps1
RUN echo "Set-PSReadLineOption -PredictionSource History" >> /root/.config/powershell/Microsoft.PowerShell_profile.ps1
RUN echo "set-PSReadLineOption -PredictionViewStyle ListView" >> /root/.config/powershell/Microsoft.PowerShell_profile.ps1
RUN echo "Set-PSReadLineOption -Colors @{'InlinePrediction'='#478390'}" >> /root/.config/powershell/Microsoft.PowerShell_profile.ps1
RUN echo "Set-PSReadLineOption -HistoryNoDuplicates" >> /root/.config/powershell/Microsoft.PowerShell_profile.ps1
RUN pwsh -Command \
    Invoke-Expression ((New-Object System.Net.WebClient).DownloadString('https://ohmyposh.dev/install.ps1'))
RUN echo "oh-my-posh --init --shell pwsh --config '/root/.config/powershell/oh-my-posh-profile.json' | invoke-expression" >> /root/.config/powershell/Microsoft.PowerShell_profile.ps1

# Run pwsh when the container launches
CMD ["pwsh"]
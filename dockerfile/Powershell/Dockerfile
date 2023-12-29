# Use an official Python runtime as a parent image
FROM mcr.microsoft.com/powershell

# Install AzCLI
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash

# Install latest AZ module from powershell gallery
RUN pwsh -Command \
    Install-Module -Name az -Force

# Install latest Microsoft.Graph module from powershell gallery
RUN pwsh -Command \
    Install-Module -Name Microsoft.Graph -Force

# Install latest PnP.Powershell module from powershell gallery
# You can specify powershell version by using parameter: -RequiredVersion
# Here you can find PnP.Powershell versions: https://github.com/pnp/powershell/releases
RUN pwsh -Command \
    Install-Module -Name PnP.Powershell -Force

# Run pwsh when the container launches
CMD ["pwsh"]
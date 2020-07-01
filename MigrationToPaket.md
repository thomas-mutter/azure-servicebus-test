# New Azure Function Project
In VS2019 a new Azure Function Project has been created from template with
a Service Bus Trigger as entry point.

# Migrate Project to paket
```powershell
dotnet new tool-manifest
dotnet tool install paket
dotnet tool restore
dotnet paket init
dotnet paket convert-from-nuget
```

At this time, current version is: Paket version 5.247.4

Findings:
- csproj: TargetFramework=netcoreapp2.1
- paket.dependencies: framework: netcoreapp3.1, netstandard2.0, netstandard2.1

So no packages are actually referenced in the project and build fails.

```powershell
dotnet paket install
```

Build the solution
```powershell
PS D:\ServiceBusTest> dotnet build                                                                                                                                                                                                                    Microsoft (R) Build Engine version 16.5.0+d4cbfca49 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Paket version 5.247.4
  The last restore is still up to date. Nothing left to do.
  Performance:
   - Runtime: 199 milliseconds
  Paket version 5.247.4
  Starting restore process.
  Performance:
   - Runtime: 1 second
  Restore completed in 966.18 ms for D:\Projekt DL\DataLogistics\ServiceBusTest\ServiceBusTest.csproj.
  Unable to use package assets cache due to I/O error. This can occur when the same project is built more than once in parallel. Performance may be degraded, but the build result will not be impacted.
  ServiceBusTest -> D:\Projekt DL\DataLogistics\ServiceBusTest\bin\Debug\netcoreapp2.1\bin\ServiceBusTest.dll
C:\Users\thomas.mutter\.nuget\packages\microsoft.azure.webjobs.script.extensionsmetadatagenerator\1.1.8\build\Microsoft.Azure.WebJobs.Script.ExtensionsMetadataGenerator.targets(37,5): warning :     Could not evaluate 'Microsoft.Win32.Registry.dll' for extension metadata. Exception message: Could not load file or assembly 'Microsoft.Win32.Registry, Version=4.1.3.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a'. [D:\ServiceBusTest\ServiceBusTest.csproj]

Build succeeded.

C:\Users\thomas.mutter\.nuget\packages\microsoft.azure.webjobs.script.extensionsmetadatagenerator\1.1.8\build\Microsoft.Azure.WebJobs.Script.ExtensionsMetadataGenerator.targets(37,5): warning :     Could not evaluate 'Microsoft.Win32.Registry.dll' for extension metadata. Exception message: Could not load file or assembly 'Microsoft.Win32.Registry, Version=4.1.3.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a'. [D:\ServiceBusTest\ServiceBusTest.csproj]
    1 Warning(s)
    0 Error(s)

Time Elapsed 00:00:09.50
```
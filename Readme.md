# HOW TO BUILD PLUGINS ON MAC

#### INSTALL TOOLS
1) brew install mono
2) Install nuget

#### CREATE PROJECT
```
mkdir "myproject"
cd "myproject"
touch "MyClassLibrary.csproj"
```

1) Fill your .csproj with the following:
(TARGET FRAMEWORK MUST BE 4.6.2)
```
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>net462</TargetFramework>
  </PropertyGroup>
</Project>
```
4) Run the following commands:
```
mono build "MyClassLibrary.csproj"
nuget restore "MyClassLibrary.csproj"
mono build "MyClassLibrary.csproj"
```
#### ADDING PACKAGES

1) Install the following packages (Check the version on nuget)
```
 dotnet add package Microsoft.CrmSdk.XrmTooling.PluginRegistrationTool --version 9.1.0.184
 dotnet add package Microsoft.CrmSdk.CoreAssemblies --version 9.0.2.50
```
2) YOU MUST MANUALY ADD REFERENCE TO nuget DLL IN <HintPath> in .csproj
(By default .nuget on root with all the installed packages)

**Replace your csproj by the following**

```
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>net462</TargetFramework>
  </PropertyGroup>
  <ItemGroup>
    <Reference Include="Microsoft.Xrm.Sdk">
      <HintPath>path/to/Microsoft.Xrm.Sdk.dll</HintPath>
    </Reference>
  </ItemGroup>
</Project>
```

#### START YOUR DEVELOPMENT

See HelloPlugin.cs file

#### Build and Sign your assembly

1) Sign your assembly:
```
sn -k keypair.snk
```

2) Add the following lines to the .csproj file:
```
<PropertyGroup>
  <SignAssembly>true</SignAssembly>
  <AssemblyOriginatorKeyFile>keypair.snk</AssemblyOriginatorKeyFile>
</PropertyGroup>
```

3) Verify that the assembly is correctly signed
```
sn -v bin/Debug/yourAssembly.dll
```

4) Build your project:
```
msbuild "YourFile.csproj" OR dotnet build
```

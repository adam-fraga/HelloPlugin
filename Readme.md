# HOW TO BUILD PLUGINS ON MAC

1) brew install mono
2) Install nuget
3) Create a file "MyClassLibrary.csproj" and fill it with:
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
(IF ERR)
nuget restore "MyClassLibrary.csproj"
mono build "MyClassLibrary.csproj"
```


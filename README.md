## MSBuild RemoteReference SDK
This is a MSBuild Sdk that allows projects to declare references to remote assets.

### Usage
On your MSBuild project insert:
```xml
    <Sdk Name="SagMor.MSBuild.RemoteReference" Version="0.1.3" />

    <ItemGroup>
        <RemoteReference Include="<Identifier>"
            Uri="<Uri>"
            Hash="<SHA256 Hash>" />
    </ItemGroup>
```

And MSBuild will download the file to the `$(BaseRemoteReferencePath)<Identifier>` folder


### Example
Downloading and copying helm.exe
```xml
    <Sdk Name="SagMor.MSBuild.RemoteReference" Version="0.1.3" />
    <ItemGroup>
        <RemoteReference Include="Helm"
            Uri="https://get.helm.sh/helm-v3.3.1-windows-amd64.zip"
            Hash="ee175565a81d1288769280b00ff1b78a77b225001471d0dd76117f909e707447"
            Unzip="true" />
    </ItemGroup>

    <ItemGroup>
        <None Include="$(BaseRemoteReferencePath)Helm\windows-amd64\helm.exe">
            <Link>helm.exe</Link>
            <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
        </None>
    </ItemGroup>
```

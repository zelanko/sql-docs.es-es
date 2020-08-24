---
title: Compilación de un proyecto desde la línea de comandos
description: Creación de una extensión SQL Server Database Projects desde la línea de comandos
ms.custom: seodec18
ms.date: 08/07/2020
ms.reviewer: drskwier, maghan, sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: ec3c9224e0cf93ae24ba1a4858b0299f7b303076
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180722"
---
# <a name="build-a-database-project-from-command-line"></a>Creación de un proyecto de base de datos desde la línea de comandos

Aunque la extensión SQL Database Projects para Azure Data Studio proporciona una interfaz de usuario gráfica para [crear un proyecto de base de datos](sql-database-project-extension-build.md), también hay disponible una experiencia de creación de línea de comandos para entornos Windows, macOS y Linux. En este artículo se describen los requisitos previos y la sintaxis necesarios para crear un proyecto SQL en dacpac desde la línea de comandos.

## <a name="prerequisites"></a>Requisitos previos
1. Instale y configure la [extensión Proyectos de base de datos de SQL para Azure Data Studio](sql-database-project-extension.md).

2. Los siguientes archivos dll de .NET Core y el archivo de destino `Microsoft.Data.Tools.Schema.SqlTasts.targets` son necesarios para crear un proyecto de base de datos SQL desde la línea de comandos desde todas las plataformas compatibles con la extensión de Azure Data Studio para SQL Database Projects. Estos archivos se crean mediante la extensión durante la primera compilación completada en la interfaz de Azure Data Studio y se colocan en la carpeta de la extensión en `BuildDirectory`.  Por ejemplo, en Linux, estos archivos se colocan en `~\.azuredatastudio\extensions\microsoft.sql-database-projects-x.x.x\BuildDirectory\`.  Copie estos 10 archivos en una carpeta nueva y accesible o tenga en cuenta su ubicación.  Se hará referencia a esta ubicación como `DotNet Core build folder` en este documento.
- Microsoft.Data.Tools.Schema.Sql.dll

- Microsoft.Data.Tools.Schema.Tasks.Sql.dll

- Microsoft.Data.Tools.Utilities.dll 

- Microsoft.SqlServer.Dac.dll 

- Microsoft.SqlServer.Dac.Extensions.dll 

- Microsoft.SqlServer.TransactSql.ScriptDom.dll 

- Microsoft.SqlServer.Types.dll 

- Microsoft.Data.Tools.Schema.SqlTasks.targets 

- System.ComponentModel.Composition.dll 

- Microsoft.Data.SqlClient.dll 


3. Si el proyecto se creó en Azure Data Studio, vaya directamente a la sección sobre cómo [crear el proyecto desde la línea de comandos](#build-the-project-from-the-command-line). Si el proyecto se creó en SQL Server Data Tools (SSDT), abra el proyecto en la extensión SQL Database Projects de Azure Data Studio.  Al abrir el proyecto en Azure Data Studio, se actualiza automáticamente el archivo `sqlproj` con tres modificaciones, las cuales se indican a continuación para su información:
    1. Condiciones de importación 
    ```
    <Import Condition="'$(NetCoreBuild)' == 'true'" Project="$(NETCoreTargetsPath)\Microsoft.Data.Tools.Schema.SqlTasks.targets"/> 
    <Import Condition="'$(NetCoreBuild)' != 'true' AND '$(SQLDBExtensionsRefPath)' != ''" Project="$(SQLDBExtensionsRefPath)\Microsoft.Data.Tools.Schema.SqlTasks.targets"/> 
    <Import Condition="'$(NetCoreBuild)' != 'true' AND '$(SQLDBExtensionsRefPath)' == ''" Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.SqlTasks.targets"/> 
    ```
    2. Referencia de paquete
    ```
    <ItemGroup> 
        <PackageReference Condition="'$(NetCoreBuild)' == 'true'" Include="Microsoft.NETFramework.ReferenceAssemblies" Version="1.0.0" PrivateAssets="All"/> 
    </ItemGroup> 
    ```
    3. Destino de limpieza, necesario para admitir la edición dual en SQL Server Data Tools (SSDT) y Azure Data Studio
    ```
    <Target Name="AfterClean"> 
        <Delete Files="$(BaseIntermediateOutputPath)\project.assets.json"/> 
    </Target> 
    ```

## <a name="build-the-project-from-the-command-line"></a>Creación del proyecto desde la línea de comandos
En la carpeta .NET completa, use el comando siguiente:
```
dotnet build "<sqlproj file path>" /p:NetCoreBuild=true /p:NETCoreTargetsPath="<DotNet Core build folder>"
```
Por ejemplo, desde `/usr/share/dotnet` en Linux:
```
dotnet build "/home/myuser/Documents/DatabaseProject1/DatabaseProject1.sqlproj" /p:NetCoreBuild=true /p:NETCoreTargetsPath="/home/myuser/.azuredatastudio-insiders/extensions/microsoft.sql-database-projects-0.1.2/BuildDirectory"  
```
## <a name="next-steps"></a>Pasos siguientes

- [Extensión Proyectos de base de datos de SQL para Azure Data Studio](sql-database-project-extension.md)
- [Publicación de proyectos de base de datos SQL](sql-database-project-extension-build.md#publish-a-database-project)

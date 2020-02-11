---
title: Usar grupos de archivos y archivos para almacenar datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- filegroups [SMO]
- storing data [SMO]
- files [SMO]
- files [SMO], about files
- storage [SMO]
ms.assetid: 7e2327ce-e1a6-4904-83d1-0944b24a7b43
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 270df8181fe42f48619736ba858dc0c16d9e30c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "72781813"
---
# <a name="using-filegroups-and-files-to-store-data"></a>Utilizar grupos de archivos y archivos para almacenar datos
  Los archivos de datos se utilizan para almacenar los archivos de base de datos. Los archivos de datos se subdividen en grupos de archivos. El objeto <xref:Microsoft.SqlServer.Management.Smo.Database> tiene una propiedad <xref:Microsoft.SqlServer.Management.Smo.Database.FileGroups%2A> que hace referencia a un objeto <xref:Microsoft.SqlServer.Management.Smo.FileGroupCollection>. Cada objeto <xref:Microsoft.SqlServer.Management.Smo.FileGroup> en esa colección tiene una propiedad <xref:Microsoft.SqlServer.Management.Smo.FileGroup.Files%2A>. Esta propiedad hace referencia a una colección <xref:Microsoft.SqlServer.Management.Smo.DataFileCollection> que contiene todos los archivos de datos que pertenecen a la base de datos. Un grupo de archivos se utiliza principalmente para agrupar los archivos que se utilizan para almacenar un objeto de la base de datos. Una razón para expandir un objeto de la base de datos en varios archivos es que puede mejorar el rendimiento, sobre todo si los archivos están almacenados en unidades de disco diferentes.  
  
 Cada base de datos que se crea automáticamente tiene un grupo de archivos denominado "Principal" y un archivo de datos con el mismo nombre que la base de datos. Se pueden agregar archivos y grupos adicionales a las recopilaciones.  
  
## <a name="examples"></a>Ejemplos  
 Para los siguientes ejemplos de código, deberá seleccionar el entorno de programación, la plantilla de programación y el lenguaje de programación en los que crear su aplicación. Para obtener más información, vea [crear un proyecto de Visual Basic SMO en Visual Studio .net](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) y [crear un proyecto de Visual C&#35; SMO en Visual Studio .net](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-visual-basic"></a>Agregar grupos de archivos y archivos de datos a una base de datos en Visual Basic  
 El grupo de archivos principal y el archivo de datos se crean automáticamente con valores de propiedad predeterminados. En el ejemplo de código se especifican algunos valores de propiedad que puede utilizar. De lo contrario, se utilizan los valores de propiedad predeterminados.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBFileGroups1](SMO How to#SMO_VBFileGroups1)]  -->  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-visual-c"></a>Agregar grupos de archivos y archivos de datos a una base de datos en Visual C#  
 El grupo de archivos principal y el archivo de datos se crean automáticamente con valores de propiedad predeterminados. En el ejemplo de código se especifican algunos valores de propiedad que puede utilizar. De lo contrario, se utilizan los valores de propiedad predeterminados.  
  
```csharp
{  
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a FileGroup object called SECONDARY on the database.   
            FileGroup fg1 = default(FileGroup);  
            fg1 = new FileGroup(db, "SECONDARY");  
            //Call the Create method to create the file group on the instance of SQL Server.   
            fg1.Create();  
            //Define a DataFile object on the file group and set the FileName property.   
            DataFile df1 = default(DataFile);  
            df1 = new DataFile(fg1, "datafile1");  
            df1.FileName = "c:\\Program Files\\Microsoft SQL Server\\MSSQL.1\\MSSQL\\Data\\datafile2.ndf";  
            //Call the Create method to create the data file on the instance of SQL Server.   
            df1.Create();  
        }  
```  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-powershell"></a>Agregar grupos de archivos y archivos de datos a una base de datos en PowerShell  
 El grupo de archivos principal y el archivo de datos se crean automáticamente con valores de propiedad predeterminados. En el ejemplo de código se especifican algunos valores de propiedad que puede utilizar. De lo contrario, se utilizan los valores de propiedad predeterminados.  
  
```powershell
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012.  
$db = get-item AdventureWorks2012  
  
#Create a new filegroup  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "SECONDARY"  
$fg1.Create()  
  
#Define a DataFile object on the file group and set the FileName property.   
$df1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.DataFile -argumentlist $fg1, "datafile1"  
  
#Make sure to have a directory created to hold the designated data file  
$df1.FileName = "c:\\TestData\\datafile2.ndf"  
  
#Call the Create method to create the data file on the instance of SQL Server.   
$df1.Create()  
```  
  
## <a name="creating-altering-and-removing-a-log-file-in-visual-basic"></a>Crear, modificar y quitar un archivo de registro en Visual Basic  
 En el ejemplo de código se crea un objeto <xref:Microsoft.SqlServer.Management.Smo.LogFile>, se cambia una de las propiedades y, a continuación, se quita el objeto de la base de datos.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBFileGroups3](SMO How to#SMO_VBFileGroups3)]  -->  
  
## <a name="creating-altering-and-removing-a-log-file-in-visual-c"></a>Crear, modificar y quitar un archivo de registro en Visual C#  
 En el ejemplo de código se crea un objeto <xref:Microsoft.SqlServer.Management.Smo.LogFile>, se cambia una de las propiedades y, a continuación, se quita el objeto de la base de datos.  
  
```csharp
//Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a LogFile object and set the database, name, and file name properties in the constructor.   
            LogFile lf1 = default(LogFile);  
            lf1 = new LogFile(db, "logfile1", "c:\\Program Files\\Microsoft SQL Server\\MSSQL.10_50.MSSQLSERVER\\MSSQL\\Data\\logfile1.ldf");  
            //Set the file growth to 6%.   
            lf1.GrowthType = FileGrowthType.Percent;  
            lf1.Growth = 6;  
            //Run the Create method to create the log file on the instance of SQL Server.   
            lf1.Create();  
            //Alter the growth percentage.
            lf1.Growth = 7;  
            lf1.Alter();  
            //Remove the log file.
            lf1.Drop();
```  
  
## <a name="creating-altering-and-removing-a-log-file-in-powershell"></a>Crear, modificar y quitar un archivo de registro en PowerShell  
 En el ejemplo de código se crea un objeto <xref:Microsoft.SqlServer.Management.Smo.LogFile>, se cambia una de las propiedades y, a continuación, se quita el objeto de la base de datos.  
  
```powershell
#Load the assembly containing the enums used in this example  
[reflection.assembly]::LoadWithPartialName("Microsoft.SqlServer.SqlEnum")  
  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012  
$db = get-item AdventureWorks2012  
  
#Create a filegroup  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Secondary"  
  
#Call the Create method to create the file group on the instance of SQL Server.   
$fg1.Create()  
  
#Define a LogFile object on the file group and set the FileName property.   
$lf1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LogFile -argumentlist $db, "LogFile2"  
  
#Set a location for it - make sure the directory exists  
$lf1.FileName = "logfile1", "c:\\Program Files\\Microsoft SQL Server\\MSSQL.10_50.MSSQLSERVER\\MSSQL\\Data\\logfile1.ldf"  
  
#Set file growth to 6%  
$lf1.GrowthType = [Microsoft.SqlServer.Management.Smo.FileGrowthType]::Percent  
$lf1.Growth = 6.0  
  
#Call the Create method to create the data file on the instance of SQL Server.   
$lf1.Create()  
  
#Alter a value and drop the log file  
$lf1.Growth = 7.0  
$lf1.Alter()  
$lf1.Drop()
```  
  
## <a name="see-also"></a>Consulte también  
 <xref:Microsoft.SqlServer.Management.Smo.FileGroup>   
 [Archivos y grupos de archivos de base de datos](../../databases/database-files-and-filegroups.md)  

---
title: Uso de particiones de índice de tabla e | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- partitions [SMO]
- storing data [SMO]
- partitioned tables [SQL Server], SMO
- partitioned indexes [SQL Server], SMO
ms.assetid: 0e682d7e-86c3-4d73-950d-aa692d46cb62
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: c3fa6b2936e5655653f2e0a20861a7d553934d19
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39554436"
---
# <a name="using-table-and-index-partitioning"></a>Utilizar particiones de tabla e índice
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Se pueden almacenar datos mediante el uso de los algoritmos de almacenamiento proporcionados por [Partitioned Tables and Indexes](../../../relational-databases/partitions/partitioned-tables-and-indexes.md). Las particiones pueden hacer que las tablas y los índices grandes sean más escalables y fáciles de administrar.  
  
## <a name="index-and-table-partitioning"></a>Particiones de tabla e índice  
 Esta característica permite expandir el índice y los datos de la tabla en varios grupos de archivos en distintas particiones. Una función de partición define la forma de asignar las filas de una tabla o un índice a un conjunto de particiones a partir de los valores de determinadas columnas, denominadas columnas de partición. Un esquema de particiones asigna cada partición especificada con la función de partición a un grupo de archivos. Esto le permite desarrollar estrategias de archivado que permiten escalar las tablas en los grupos de archivos y por consiguiente en los dispositivos físicos.  
  
 El <xref:Microsoft.SqlServer.Management.Smo.Database> objeto contiene una colección de <xref:Microsoft.SqlServer.Management.Smo.PartitionFunction> objetos que representan las funciones de partición implementadas y una colección de <xref:Microsoft.SqlServer.Management.Smo.PartitionScheme> objetos que describen cómo los datos se asignan a grupos de archivos.  
  
 Cada objeto <xref:Microsoft.SqlServer.Management.Smo.Table> y <xref:Microsoft.SqlServer.Management.Smo.Index> especifica qué esquema de partición utiliza en la propiedad <xref:Microsoft.SqlServer.Management.Smo.PartitionScheme> y especifica las columnas en <xref:Microsoft.SqlServer.Management.Smo.PartitionSchemeParameterCollection>.  
  
## <a name="example"></a>Ejemplo  
 Para los siguientes ejemplos de código, deberá seleccionar el entorno de programación, la plantilla de programación y el lenguaje de programación en los que crear su aplicación. Para obtener más información, consulte [crear un Visual C&#35; proyecto SMO en Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="setting-up-a-partition-scheme-for-a-table-in-visual-c"></a>Configurar un esquema de partición para una tabla en Visual C#  
 El ejemplo de código muestra cómo crear una función de partición y un esquema de partición para el `TransactionHistory` tabla el [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] base de datos de ejemplo. Las particiones se dividen por fecha con la intención de separar los registros anteriores de la tabla `TransactionHistoryArchive` .  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Define and create three new file groups on the database.   
FileGroup fg2;   
fg2 = new FileGroup(db, "Second");   
fg2.Create();   
FileGroup fg3;   
fg3 = new FileGroup(db, "Third");   
fg3.Create();   
FileGroup fg4;   
fg4 = new FileGroup(db, "Fourth");   
fg4.Create();   
//Define a partition function by supplying the parent database and name arguments in the constructor.   
PartitionFunction pf;   
pf = new PartitionFunction(db, "TransHistPF");   
//Add a partition function parameter that specifies the function uses a DateTime range type.   
PartitionFunctionParameter pfp;   
pfp = new PartitionFunctionParameter(pf, DataType.DateTime);   
pf.PartitionFunctionParameters.Add(pfp);   
//Specify the three dates that divide the data into four partitions.   
object[] val;   
val = new object[] {"1/1/2003", "1/1/2004", "1/1/2005"};   
pf.RangeValues = val;   
//Create the partition function.   
pf.Create();   
//Define a partition scheme by supplying the parent database and name arguments in the constructor.   
PartitionScheme ps;   
ps = new PartitionScheme(db, "TransHistPS");   
//Specify the partition function and the filegroups required by the partition scheme.   
ps.PartitionFunction = "TransHistPF";   
ps.FileGroups.Add("PRIMARY");   
ps.FileGroups.Add("second");   
ps.FileGroups.Add("Third");   
ps.FileGroups.Add("Fourth");   
//Create the partition scheme.   
ps.Create();   
}   
```  
  
## <a name="setting-up-a-partition-scheme-for-a-table-in-powershell"></a>Configurar un esquema de partición para una tabla en PowerShell  
 El ejemplo de código muestra cómo crear una función de partición y un esquema de partición para el `TransactionHistory` tabla el [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] base de datos de ejemplo. Las particiones se dividen por fecha con la intención de separar los registros anteriores de la tabla `TransactionHistoryArchive` .  
  
```powershell  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
$db = $srv.Databases["AdventureWorks"]  
#Create four filegroups  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "First"  
$fg2 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Second"  
$fg3 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Third"  
$fg4 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Fourth"  
  
#Define a partition function by supplying the parent database and name arguments in the constructor.  
$pf =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionFunction -argumentlist $db, "TransHistPF"  
$T = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$T  
$T.GetType()  
#Add a partition function parameter that specifies the function uses a DateTime range type.  
$pfp =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionFunctionParameter -argumentlist $pf, $T  
  
#Specify the three dates that divide the data into four partitions.   
#Create an array of type object to hold the partition data  
$val = "1/1/2003"."1/1/2004","1/1/2005"  
$pf.RangeValues = $val  
$pf  
#Create the partition function  
$pf.Create()  
  
#Create partition scheme  
$ps = New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionScheme -argumentlist $db, "TransHistPS"  
$ps.PartitionFunction = "TransHistPF"  
  
#add the filegroups to the scheme   
$ps.FileGroups.Add("PRIMARY")  
$ps.FileGroups.Add("Second")  
$ps.FileGroups.Add("Third")  
$ps.FileGroups.Add("Fourth")  
  
#Create it at the server  
$ps.Create()  
```  
  
## <a name="see-also"></a>Vea también  
 [Partitioned Tables and Indexes](../../../relational-databases/partitions/partitioned-tables-and-indexes.md)  
  
  

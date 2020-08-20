---
description: Crear y actualizar estadísticas
title: Crear y actualizar estadísticas
ms.prod: sql
ms.prod_service: database-engine
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- statistical information [SMO]
ms.assetid: 47a0a172-a969-4deb-bca9-dd04401a0fe1
author: markingmyname
ms.author: maghan
ms.reviewer: matteot
ms.custom: seo-dt-2019
ms.date: 06/04/2020
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3939942c7655206a448797f0258d883eac904fef
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455516"
---
# <a name="create-and-update-statistics"></a>Crear y actualizar estadísticas

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

En SMO, la información estadística sobre las consultas de procesamiento en la base de datos se puede recopilar utilizando el objeto <xref:Microsoft.SqlServer.Management.Smo.Statistic>.

Es posible crear estadísticas para cualquier columna mediante el <xref:Microsoft.SqlServer.Management.Smo.Statistic> <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn> objeto y. El método <xref:Microsoft.SqlServer.Management.Smo.Statistic.Update%2A> se puede ejecutar para actualizar las estadísticas en el objeto <xref:Microsoft.SqlServer.Management.Smo.Statistic>. Los resultados se pueden ver en el optimizador de consultas.

## <a name="example"></a>Ejemplo

Para usar cualquier ejemplo de código que se proporcione, puede elegir el entorno de programación, la plantilla de programación y el lenguaje de programación en el que se va a crear la aplicación. Para obtener más información, vea [crear un proyecto de Visual C&#35; SMO en Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).

## <a name="create-and-update-statistics-in-visual-basic"></a>Crear y actualizar estadísticas en Visual Basic

En este ejemplo de código se crea una nueva tabla en una base de datos existente para la que se crean los objetos <xref:Microsoft.SqlServer.Management.Smo.Statistic> y <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn>.

```vb
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Reference the CreditCard table.
Dim tb As Table
tb = db.Tables("CreditCard", "Sales")
'Define a Statistic object by supplying the parent table and name arguments in the constructor.
Dim stat As Statistic
stat = New Statistic(tb, "Test_Statistics")
'Define a StatisticColumn object variable for the CardType column and add to the Statistic object variable.
Dim statcol As StatisticColumn
statcol = New StatisticColumn(stat, "CardType")
stat.StatisticColumns.Add(statcol)
'Create the statistic counter on the instance of SQL Server.
stat.Create()
```

## <a name="create-and-update-statistics-in-c"></a>Crear y actualizar estadísticas en C #

En este ejemplo de código se crea una nueva tabla en una base de datos existente para la que se crean los objetos <xref:Microsoft.SqlServer.Management.Smo.Statistic> y <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn>.

```csharp
public static void CreatingAndUpdatingStatistics()
{
    // Connect to the local, default instance of SQL Server.
    var srv = new Server();

    // Reference the AdventureWorks2012 database.
    var db = srv.Databases["AdventureWorks"];

    // Reference the CreditCard table.
    var tb = db.Tables["CreditCard", "Sales"];

    // Define a Statistic object by supplying the parent table and name
    // arguments in the constructor.
    var stat = new Statistic(tb, "Test_Statistics");

    // Define a StatisticColumn object variable for the CardType column
    // and add to the Statistic object variable.
    var statcol = new StatisticColumn(stat, "CardType");
    stat.StatisticColumns.Add(statcol);

    //Create the statistic counter on the instance of SQL Server.
    stat.Create();

    // List all the statistics object on the table (you will see the newly created one)
    foreach (var s in tb.Statistics.Cast<Statistic>())
        Console.WriteLine($"{s.ID}\t{s.Name}");

    // Output:
    //  2       AK_CreditCard_CardNumber
    //  1       PK_CreditCard_CreditCardID
    //  3       Test_Statistics
 }
```

## <a name="create-and-update-statistics-in-powershell"></a>Crear y actualizar estadísticas en PowerShell

En este ejemplo de código se crea una nueva tabla en una base de datos existente para la que se crean los objetos <xref:Microsoft.SqlServer.Management.Smo.Statistic> y <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn>.

```powershell
Import-Module SQLServer

# Connect to the local, default instance of SQL Server.  
$srv = Get-Item SQLSERVER:\SQL\localhost\DEFAULT

# Reference the AdventureWorks database.
$db = $srv.Databases["AdventureWorks"]

# Reference the CreditCard table.
$tb = $db.Tables["CreditCard", "Sales"]

# Define a Statistic object by supplying the parent table and name
# arguments in the constructor.
$stat = New-Object Microsoft.SqlServer.Management.Smo.Statistic($tb, "Test_Statistics")

# Define a StatisticColumn object variable for the CardType column
# and add to the Statistic object variable.
$statcol = New-Object Microsoft.SqlServer.Management.Smo.StatisticColumn($stat, "CardType")
$stat.StatisticColumns.Add($statcol)

# Create the statistic counter on the instance of SQL Server.
$stat.Create()

# Finally dump all the statistics (you can see the newly created one at the bottom)
$tb.Statistics

# Output:
# Name                                Last Updated Is From Index  Statistic Columns
#                                                  Creation
# ----                                ------------ -------------- -----------------
# AK_CreditCard_CardNumber      10/27/2017 2:33 PM True           {CardNumber}
# PK_CreditCard_CreditCardID    10/27/2017 2:33 PM True           {CreditCardID}
# Test_Statistics                 6/4/2020 8:11 PM False          {CardType}
```

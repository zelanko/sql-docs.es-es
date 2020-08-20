---
description: Usar sinónimos
title: Usar sinónimos | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- synonyms [SMO]
ms.assetid: db0a9022-9549-43e5-b6b3-deb236f05fb8
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7fef9446721928315268db66d46af6ed3a4138c1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464957"
---
# <a name="using-synonyms"></a>Usar sinónimos
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  Un sinónimo es un nombre alternativo para un objeto de ámbito de esquema. En SMO, el objeto <xref:Microsoft.SqlServer.Management.Smo.Synonym> representa los sinónimos. El objeto <xref:Microsoft.SqlServer.Management.Smo.Synonym> es un elemento secundario del objeto <xref:Microsoft.SqlServer.Management.Smo.Database>. Esto significa que los sinónimos solo son válidos dentro del ámbito de la base de datos en la que se definen. Sin embargo, el sinónimo puede hacer referencia a los objetos en otra base de datos o en una instancia remota de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 El objeto al que se proporciona un nombre alternativo se conoce como el objeto base. La propiedad de nombre del objeto <xref:Microsoft.SqlServer.Management.Smo.Synonym> es el nombre alternativo dado al objeto base.  
  
## <a name="example"></a>Ejemplo  
 Para los siguientes ejemplos de código, deberá seleccionar el entorno de programación, la plantilla de programación y el lenguaje de programación en los que crear su aplicación. Para obtener más información, vea [crear un proyecto de Visual C&#35; SMO en Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-synonym-in-visual-c"></a>Crear un sinónimo en Visual C#  
 En el ejemplo de código se muestra cómo crear un sinónimo o un nombre alternativo para un objeto de ámbito de esquema. Las aplicaciones cliente pueden utilizar una única referencia para un objeto base utilizando un sinónimo en lugar de utilizar un nombre de varias partes para hacer referencia al objeto base.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
  
            //Reference the AdventureWorks2012 database.   
            Database db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Synonym object variable by supplying the   
            //parent database, name, and schema arguments in the constructor.   
            //The name is also a synonym of the name of the base object.   
            Synonym syn = new Synonym(db, "Shop", "Sales");  
  
            //Specify the base object, which is the object on which   
            //the synonym is based.   
            syn.BaseDatabase = "AdventureWorks2012";  
            syn.BaseSchema = "Sales";  
            syn.BaseObject = "Store";  
            syn.BaseServer = srv.Name;  
  
            //Create the synonym on the instance of SQL Server.   
            syn.Create();  
        }  
```  
  
## <a name="creating-a-synonym-in-powershell"></a>Crear un sinónimo en PowerShell  
 En el ejemplo de código se muestra cómo crear un sinónimo o un nombre alternativo para un objeto de ámbito de esquema. Las aplicaciones cliente pueden utilizar una única referencia para un objeto base utilizando un sinónimo en lugar de utilizar un nombre de varias partes para hacer referencia al objeto base.  
  
```powershell  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#And the database object corresponding to Adventureworks  
$db = $srv.Databases["AdventureWorks2012"]  
  
$syn = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Synonym `  
-argumentlist $db, "Shop", "Sales"  
  
#Specify the base object, which is the object on which the synonym is based.  
$syn.BaseDatabase = "AdventureWorks2012"  
$syn.BaseSchema = "Sales"  
$syn.BaseObject = "Store"  
$syn.BaseServer = $srv.Name  
  
#Create the synonym on the instance of SQL Server.  
$syn.Create()  
```  
  
## <a name="see-also"></a>Consulte también  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](../../../t-sql/statements/create-synonym-transact-sql.md)  
  
  

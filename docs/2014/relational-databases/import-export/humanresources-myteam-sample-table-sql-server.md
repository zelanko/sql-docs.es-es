---
title: Tabla de ejemplo HumanResources.myTeam (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- myTeam sample table [SQL Server]
- bulk importing [SQL Server], examples
- bulk exporting [SQL Server], examples
ms.assetid: 27da45a0-c1f4-4bf4-ab24-6196e80d3834
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5628df909bc5d28706ab6c9032f6dc62a13489c3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48109437"
---
# <a name="humanresourcesmyteam-sample-table-sql-server"></a>Tabla de ejemplo HumanResources.myTeam (SQL Server)
  Muchos de los ejemplos de código de [Importar y exportar datos masivos](bulk-import-and-export-of-data-sql-server.md) requieren una tabla de prueba especial llamada **myTeam**. Antes de poder ejecutar los ejemplos, debe crear la tabla **myTeam** en el esquema **HumanResources** de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
> [!NOTE]  
>  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] es una de las bases de datos de ejemplo de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 La tabla **myTeam** contiene las columnas siguientes.  
  
|columna|Tipo de datos|Nulabilidad|Descripción|  
|------------|---------------|-----------------|-----------------|  
|**EmployeeID**|`smallint`|No NULL|Clave principal para las filas. Identificador de empleado de un miembro de mi equipo.|  
|**Nombre**|`nvarchar(50)`|No NULL|Nombre de un miembro de mi equipo.|  
|**Title**|`nvarchar(50)`|Admisión de valores NULL|Cargo que tiene el empleado en mi equipo.|  
|**Información previa**|`nvarchar(50)`|No NULL|Fecha y hora de la última actualización de la fila. (Es el valor predeterminado).|  
  
 **Para crear HumanResources.myTeam**  
  
-   Utilice las siguientes instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    ```  
    --Create HumanResources.MyTeam:   
    USE AdventureWorks;  
    GO  
    CREATE TABLE HumanResources.myTeam   
    (EmployeeID smallint NOT NULL,  
    Name nvarchar(50) NOT NULL,  
    Title nvarchar(50) NULL,  
    Background nvarchar(50) NOT NULL DEFAULT ''  
    );  
    GO  
    ```  
  
 **Para rellenar HumanResources.myTeam**  
  
-   Ejecute las siguientes instrucciones `INSERT` para rellenar la tabla con dos filas:  
  
    ```  
    USE AdventureWorks;  
    GO  
    INSERT INTO HumanResources.myTeam(EmployeeID,Name,Title,Background)  
       VALUES(77,'Mia Doppleganger','Administrative Assistant','Microsoft Office');  
    GO  
    INSERT INTO HumanResources.myTeam(EmployeeID,Name,Title,Background)  
       VALUES(49,'Hirum Mollicat','I.T. Specialist','Report Writing and Data Mining');  
    GO  
    ```  
  
    > [!NOTE]  
    >  Estas instrucciones omiten la cuarta columna, `Background`. Tiene un valor predeterminado. Omitir esta columna hace que esta instrucción `INSERT` deje la columna en blanco.  
  
## <a name="see-also"></a>Vea también  
 [Importar y exportar datos en bloque &#40;SQL Server&#41;](bulk-import-and-export-of-data-sql-server.md)  
  
  

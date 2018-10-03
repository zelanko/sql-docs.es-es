---
title: Utilice sp_rename para cambiar el nombre de índice duplicados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- table names [SQL Server]
- duplicate table names
- index names [SQL Server]
- sp_rename
- duplicate index names
ms.assetid: ee66c7a5-eb6d-4fcf-970c-ab099d78c8d9
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 641dbb6e33f7b39a7542fdd43a940c487a4b21d9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48093045"
---
# <a name="use-sprename-to-rename-duplicate-index-name"></a>Utilizar sp_rename para cambiar el nombre de índice duplicado
  El Asesor de actualizaciones ha detectado nombres de índice de vista o tabla duplicados. Cambie los nombres de los índices o quite los duplicados antes de actualizar.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
  
1.  Localice los índices duplicados ejecutando la siguiente consulta.  
  
    ```  
    SELECT DISTINCT OBJECT_NAME(o.id), name  
    FROM sysindexes as o  
    WHERE EXISTS   
        (SELECT name FROM sysindexes  as i  
          WHERE i.id = o.id  
          AND i.name = o.name and i.indid < o.indid);  
    ```  
  
2.  Utilice **sp_rename** para cambiar uno de los nombres de índice. Como los nombres de índice son los mismos, no puede determinar qué índice cambiará de nombre. Este paso le permite diferenciar los índices.  
  
    ```  
    EXEC sp_rename N'table_name.index_name', N'new_index_name', N'INDEX'  
    ```  
  
3.  Compruebe qué índice ha cambiado de nombre ejecutando la siguiente consulta. Esta consulta devuelve todos los índices (incluidos los nombres de columnas de clave) de la vista o tabla especificada.  
  
    ```  
    SELECT i.name AS IndexName, c.name AS ColumnName, ik.colid, ik.keyno  
    FROM sysindexes i  
    JOIN sysindexkeys ik ON i.id = ik.id and i.indid = ik.indid   
    JOIN syscolumns c ON c.id = ik.id and ik.colid = c.colid  
    WHERE i.id = OBJECT_ID('table_or_view_name')  
    ```  
  
4.  Si fuera necesario, utilice de nuevo **sp_rename** para corregir los nombres de índice.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  

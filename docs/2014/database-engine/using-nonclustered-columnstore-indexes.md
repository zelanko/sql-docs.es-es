---
title: El uso de índices de almacén de columnas no agrupado | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4c341fb8-7cb1-4cab-921b-e80b751d6c19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f32acde4b49b8b4b91c087fb66e41d4c2cf276ce
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37157026"
---
# <a name="using-nonclustered-columnstore-indexes"></a>Usar índices no clúster de almacén de columnas
  Describe las tareas clave para utilizar un índice no clúster de almacén de columnas en una tabla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Para obtener información general de los índices de almacén de columnas, vea [Columnstore Indexes Described](../relational-databases/indexes/columnstore-indexes-described.md).  
  
 Para obtener información acerca de los índices de almacén de columnas agrupado, vea [Using Clustered Columnstore Indexes](../relational-databases/indexes/indexes.md).  
  
## <a name="contents"></a>Contenido  
  
-   [Crear un índice no agrupado de almacén de columnas](../../2014/database-engine/using-nonclustered-columnstore-indexes.md#load)  
  
-   [Cambiar los datos de un índice no agrupado de almacén de columnas](../../2014/database-engine/using-nonclustered-columnstore-indexes.md#change)  
  
##  <a name="load"></a> Crear un índice no agrupado de almacén de columnas  
 Para cargar datos en un índice de almacén, cargue primero los datos en una tabla tradicional de almacén de filas almacenada como un montón o agrupado de índice y, a continuación, usar [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-columnstore-index-transact-sql) para crear un índice de almacén de columnas.  
  
 ![Cargar datos en un índice de almacén de columnas](../../2014/database-engine/media/sql-server-pdw-columnstore-loadprocess-nonclustered.gif "cargar datos en un índice de almacén de columnas")  
  
##  <a name="change"></a> Cambiar los datos de un índice no agrupado de almacén de columnas  
 Una vez creado un índice no clúster de almacén de columnas en una tabla, no puede modificar directamente los datos de esa tabla. Una consulta con INSERT, UPDATE, DELETE o MERGE generará un error y devolverá un mensaje de error. Para agregar o modificar los datos de la tabla, puede hacer lo siguiente:  
  
-   Deshabilitar el índice de almacén de columnas. Después puede actualizar los datos de la tabla. Si deshabilita el índice de almacén de columnas, puede regenerar el índice de almacén de columnas cuando termine de actualizar los datos. Por ejemplo:  
  
    ```  
    ALTER INDEX mycolumnstoreindex ON mytable DISABLE;  
    -- update mytable --  
    ALTER INDEX mycolumnstoreindex on mytable REBUILD  
    ```  
  
-   Quite el índice de almacén de columnas, actualizar la tabla y, a continuación, volver a crear el índice de almacén de columnas con CREATE COLUMNSTORE INDEX. Por ejemplo:  
  
    ```  
    DROP INDEX mycolumnstoreindex ON mytable  
    -- update mytable --  
    CREATE NONCLUSTERED COLUMNSTORE INDEX mycolumnstoreindex ON mytable;  
  
    ```  
  
-   Cargar datos en una tabla de ensayo que no tenga un índice de almacén de columnas. Genere un índice de almacén de columnas en la tabla de ensayo. Cambie la tabla de ensayo a una partición vacía de la tabla principal.  
  
-   Cambiar una partición de la tabla con el índice de almacén de columnas a una tabla de ensayo vacía. Si hay un índice de almacén de columnas en la tabla de ensayo, deshabilítelo. Realice las actualizaciones que desee. Genere (o regenere) el índice de almacén de columnas. Vuelva a cambiar la tabla de ensayo a la partición (ahora vacía) de la tabla principal.  
  

  
  

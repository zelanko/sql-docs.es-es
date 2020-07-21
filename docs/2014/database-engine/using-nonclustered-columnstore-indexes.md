---
title: Uso de índices de almacén de columnas no agrupados | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 4c341fb8-7cb1-4cab-921b-e80b751d6c19
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: c876eb6fdd466349ac369dcff8e292bc0839c669
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84927787"
---
# <a name="using-nonclustered-columnstore-indexes"></a>Usar índices no clúster de almacén de columnas
  Describe las tareas clave para utilizar un índice no clúster de almacén de columnas en una tabla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .

 Para obtener información general acerca de los índices de almacén de columnas, vea [Columnstore Indexes Described](../relational-databases/indexes/columnstore-indexes-described.md).

 Para obtener información acerca de los índices clúster de almacén de columnas, vea [Using Clustered Columnstore Indexes](../relational-databases/indexes/indexes.md).

## <a name="contents"></a>Contenido

-   [Crear un índice no clúster de almacén de columnas](../../2014/database-engine/using-nonclustered-columnstore-indexes.md#load)

-   [Cargar los datos en un índice no clúster de almacén de columnas](../../2014/database-engine/using-nonclustered-columnstore-indexes.md#change)

##  <a name="create-a-nonclustered-columnstore-index"></a><a name="load"></a>Crear un índice de almacén de columnas no agrupado
 Para cargar datos en un índice de almacén de columnas no agrupado, cargue primero los datos en una tabla almacén tradicional almacenada como un montón o un índice clúster y, a continuación, use [crear índice de almacén de columnas &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql) para crear un índice de almacén de columnas.

 ![Cargar datos en un índice de almacén de columnas](../../2014/database-engine/media/sql-server-pdw-columnstore-loadprocess-nonclustered.gif "Cargar datos en un índice de almacén de columnas")

##  <a name="change-the-data-in-a-nonclustered-columnstore-index"></a><a name="change"></a>Cambiar los datos de un índice de almacén de columnas no agrupado
 Una vez creado un índice no clúster de almacén de columnas en una tabla, no puede modificar directamente los datos de esa tabla. Una consulta con INSERT, UPDATE, DELETE o MERGE generará un error y devolverá un mensaje de error. Para agregar o modificar los datos de la tabla, puede hacer lo siguiente:

-   Deshabilite el índice de almacén de columnas. Después puede actualizar los datos de la tabla. Si deshabilita el índice de almacén de columnas, puede regenerar el índice de almacén de columnas cuando termine de actualizar los datos. Por ejemplo:

    ```
    ALTER INDEX mycolumnstoreindex ON mytable DISABLE;
    -- update mytable --
    ALTER INDEX mycolumnstoreindex on mytable REBUILD
    ```

-   Quite el índice de almacén de columnas, actualice la tabla y, a continuación, vuelva a crear el índice de almacén de columnas con crear índice de almacén de columnas. Por ejemplo:

    ```
    DROP INDEX mycolumnstoreindex ON mytable
    -- update mytable --
    CREATE NONCLUSTERED COLUMNSTORE INDEX mycolumnstoreindex ON mytable;

    ```

-   Cargar datos en una tabla de ensayo que no tenga un índice de almacén de columnas. Genere un índice de almacén de columnas en la tabla de ensayo. Cambie la tabla de ensayo a una partición vacía de la tabla principal.

-   Cambiar una partición de la tabla con el índice de almacén de columnas a una tabla de ensayo vacía. Si hay un índice de almacén de columnas en la tabla de ensayo, deshabilítelo. Realice las actualizaciones que desee. Genere (o regenere) el índice de almacén de columnas. Vuelva a cambiar la tabla de ensayo a la partición (ahora vacía) de la tabla principal.





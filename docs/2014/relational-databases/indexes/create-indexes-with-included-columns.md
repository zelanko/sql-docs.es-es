---
title: Creación de índices con columnas incluidas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index size [SQL Server]
- index keys [SQL Server]
- index columns [SQL Server]
- size [SQL Server], indexes
- key columns [SQL Server]
- included columns
- nonclustered indexes [SQL Server], included columns
- designing indexes [SQL Server], included columns
- nonkey columns
ms.assetid: d198648d-fea5-416d-9f30-f9d4aebbf4ec
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5c0c6449082f1c5ca016cfdb0a0f18430cf74731
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63156812"
---
# <a name="create-indexes-with-included-columns"></a>Crear índices con columnas incluidas
  En este tema se describe cómo agregar columnas incluidas (o sin clave) para ampliar la funcionalidad de índices no clúster en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Al incluir columnas sin clave, puede crear índices no clúster que abarcan más consultas. Esto se debe a que las columnas sin clave tienen las siguientes ventajas:  
  
-   Pueden ser tipos de datos que no están permitidos como columnas de clave de índice.  
  
-   El [!INCLUDE[ssDE](../../includes/ssde-md.md)] no las tiene en cuenta cuando calcula el número de columnas de clave de índice o el tamaño de las claves de índice.  
  
 Un índice con columnas sin clave puede mejorar significativamente el rendimiento de una consulta cuando todas las columnas de la consulta se incluyen como columnas de clave o columnas sin clave. Las mejoras en el rendimiento se consiguen porque el optimizador de consultas puede localizar todos los valores de las columnas del índice, sin tener acceso a los datos de la tabla o del índice clúster, lo que da como resultado menos operaciones de E/S de disco.  
  
> [!NOTE]  
>  Cuando un índice contiene todas las columnas a las que hace referencia una consulta, normalmente se dice que *abarca la consulta*.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones de diseño](#DesignRecs)  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para crear un índice con columnas sin clave, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="design-recommendations"></a><a name="DesignRecs"></a> Recomendaciones de diseño  
  
-   Rediseñe índices no clúster con un tamaño de las claves de índice grande para que solo las columnas utilizadas para búsquedas sean columnas de clave. Convierta todas las demás columnas que abarcan la consulta en columnas sin clave. De esta forma, tendrá todas las columnas necesarias para abarcar la consulta pero la clave de índice en sí será pequeña y eficaz.  
  
-   Incluya columnas sin clave en un índice no clúster para evitar que se superen las limitaciones actuales de tamaño del índice de un máximo de 16 columnas de clave y un tamaño máximo de clave de índice de 900 bytes. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] no tiene en cuenta las columnas sin clave al calcular el número de columnas de clave de índice o el tamaño de las claves de índice.  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Las columnas sin clave solo pueden definirse en índices no clúster.  
  
-   Todos los tipos de datos excepto `text`, `ntext` e `image` se pueden usar como columnas sin clave.  
  
-   Las columnas calculadas que son deterministas, y precisas o imprecisas, pueden ser columnas sin clave. Para obtener más información, vea [Indexes on Computed Columns](indexes-on-computed-columns.md).  
  
-   Las columnas calculadas derivadas de los tipos de datos `image`, `ntext` y `text` pueden ser columnas sin clave siempre que se permita el tipo de datos de la columna calculada como columna de índice sin clave.  
  
-   Las columnas sin clave no se pueden quitar de una tabla, a menos que antes se quite el índice de la tabla.  
  
-   Las columnas sin clave no se pueden cambiar, excepto para hacer lo siguiente:  
  
    -   Cambiar la nulabilidad de NOT NULL a NULL.  
  
    -   Aumentar la longitud de las columnas `varchar`, `nvarchar` o `varbinary`.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla o la vista. El usuario debe ser miembro del rol fijo de servidor **sysadmin** o de los roles fijos de base de datos **db_ddladmin** y **db_owner** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-create-an-index-with-nonkey-columns"></a>Para crear un índice con columnas sin clave  
  
1.  En el Explorador de objetos, haga clic en el signo más para expandir la base de datos que contiene la tabla en la que desea crear un índice con columnas sin clave.  
  
2.  Haga clic en el signo más para expandir la carpeta **Tablas** .  
  
3.  Haga clic en el signo más para expandir la tabla en la que desea crear un índice con columnas sin clave.  
  
4.  Haga clic con el botón secundario en la carpeta **índices** , seleccione **nuevo índice**y seleccione **índice no clúster..**..  
  
5.  En el cuadro de diálogo **Nuevo índice** , en la página **General** , escriba el nombre del nuevo índice en el cuadro **Nombre de índice** .  
  
6.  En la pestaña **Columnas de clave de índice**, haga clic en **Agregar...**.  
  
7.  En el cuadro de diálogo **seleccionar columnas de**_TABLE_NAME_ , active las casillas de las columnas de tabla que se van a agregar al índice.  
  
8.  Haga clic en **Aceptar**.  
  
9. En la pestaña **Columnas incluidas**, haga clic en **Agregar...**.  
  
10. En el cuadro de diálogo **seleccionar columnas de**_TABLE_NAME_ , active las casillas de las columnas de tabla que se van a agregar al índice como columnas sin clave.  
  
11. Haga clic en **Aceptar**.  
  
12. En el cuadro de diálogo **Nuevo índice** , haga clic en **Aceptar**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-create-an-index-with-nonkey-columns"></a>Para crear un índice con columnas sin clave  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Creates a nonclustered index on the Person.Address table with four included (nonkey) columns.   
    -- index key column is PostalCode and the nonkey columns are  
    -- AddressLine1, AddressLine2, City, and StateProvinceID.  
    CREATE NONCLUSTERED INDEX IX_Address_PostalCode  
    ON Person.Address (PostalCode)  
    INCLUDE (AddressLine1, AddressLine2, City, StateProvinceID);  
    GO  
    ```  
  
 Para obtener más información, vea [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql).  
  
  

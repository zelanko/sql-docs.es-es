---
title: "Creación de índices clúster | Microsoft Docs"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- index creation [SQL Server], clustered indexes
- clustered indexes, creating
- clustered indexes, PRIMARY KEY constraint
- clustered indexes, UNIQUE constraint
- indexes [SQL Server], clustered
ms.assetid: 47148383-c2c7-4f08-a9e4-7016bf2d1d13
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: ec406af911a0ea95910eba4a7bf35b68544418cd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="create-clustered-indexes"></a>Crear índices clúster
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Puede crear índices clúster en las tablas mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Con pocas excepciones, todas las tablas deben tener un índice clúster. Además de mejorar el rendimiento de las consultas, un índice clúster se puede recompilar o reorganizar a petición para controlar la fragmentación de las tablas. También se puede crear un índice clúster en una vista. (Los índices agrupados se definen en el tema [Índices agrupados y no agrupados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Implementaciones típicas](#Implementations)  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para crear un índice clúster en una tabla, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Implementations"></a> Implementaciones típicas  
 Los clúster se implementan de las formas siguientes:  
  
-   **Restricciones PRIMARY KEY y UNIQUE**  
  
     Cuando se crea una restricción PRIMARY KEY, se crea automáticamente un índice clúster único en las columnas si aún no existe un índice clúster en la tabla o no se ha especificado un índice no clúster. La columna de clave principal no puede permitir valores NULL.  
  
     Cuando cree una restricción UNIQUE, se creará un índice no clúster único para exigir una restricción UNIQUE de forma predeterminada. Puede especificarse un índice clúster único si todavía no existe un índice clúster en la tabla.  
  
     Un índice creado como parte de la restricción recibe automáticamente el mismo nombre que la restricción. Para obtener más información, consulte [Primary and Foreign Key Constraints](../../relational-databases/tables/primary-and-foreign-key-constraints.md) y [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md).  
  
-   **Índice independiente de una restricción**  
  
     Puede crear un índice clúster en una columna que no sea la de clave principal si se especificó una restricción de clave principal no agrupada.  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Cuando se crea una estructura de índice clúster, se requiere espacio en disco para ambas estructuras, la antigua (origen) y la nueva (destino), en los archivos y grupos de archivos correspondientes. La asignación de la antigua estructura no se cancela hasta que se valide la transacción completa. Puede que también se necesite espacio en disco temporal para ordenar. Para más información, consulte [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md).  
  
-   Si se crea un índice clúster en un montón con varios índices no clúster existentes, se deben volver a generar todos los índices no clúster de manera que contengan el valor de clave de agrupación en clústeres en lugar del identificador de fila (RID). De forma similar, si se quita un índice clúster de una tabla con varios índices no clúster, se vuelven a generar todos los índices no clúster como parte de la operación DROP. Si las tablas son de gran tamaño, la operación puede prolongarse significativamente.  
  
     La mejor manera de generar índices en tablas de gran tamaño es empezar con el índice clúster y, a continuación, generar los índices no clúster. Considere la posibilidad de establecer la opción ONLINE en ON al crear índices en tablas existentes. Cuando se establece en ON, no se mantienen los bloqueos de tabla de larga duración. Así se habilita la continuación de consultas o actualizaciones de la tabla subyacente. Para más información, consulte [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
-   La clave de índice de un índice agrupado no puede contener columnas **varchar** con datos existentes en la unidad de asignación ROW_OVERFLOW_DATA. Si se crea un índice agrupado en una columna **varchar** y los datos existentes están en la unidad de asignación IN_ROW_DATA, no se realizarán correctamente las siguientes acciones de inserción o actualización en la columna que intenten insertar los datos de manera no consecutiva. Para obtener información sobre las tablas que pueden contener datos de desbordamiento de fila, use la función de administración dinámica [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla o la vista. El usuario debe ser miembro del rol fijo de servidor **sysadmin** o de los roles fijos de base de datos **db_ddladmin** y **db_owner** .  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-create-a-clustered-index-by-using-object-explorer"></a>Para crear un índice clúster mediante el Explorador de objetos  
  
1.  En el Explorador de objetos, expanda la tabla en la que desea crear un índice clúster.  
  
2.  Haga clic con el botón derecho en la carpeta **Índices** , seleccione **Nuevo índice**y, luego, **Índice no agrupado…**.  
  
3.  En el cuadro de diálogo **Nuevo índice** , en la página **General** , escriba el nombre del nuevo índice en el cuadro **Nombre de índice** .  
  
4.  Debajo de **Columnas de clave de índice**, haga clic en **Agregar**.  
  
5.  En el cuadro de diálogo **Seleccionar columnas de***table_name* , active la casilla de la columna de tabla que se va a agregar al índice agrupado.  
  
6.  Haga clic en **Aceptar**.  
  
7.  En el cuadro de diálogo **Nuevo índice** , haga clic en **Aceptar**.  
  
#### <a name="to-create-a-clustered-index-by-using-the-table-designer"></a>Para crear un índice clúster mediante el Diseñador de tablas  
  
1.  En el Explorador de objetos, expanda la base de datos en la que desea crear una tabla con un índice clúster.  
  
2.  Haga clic con el botón derecho en la carpeta **Tablas** y, luego, haga clic en **Nueva tabla**.  
  
3.  Cree una tabla nueva como lo haría normalmente. Para obtener más información, vea [Crear tablas &#40;motor de base de datos&#41;](../../relational-databases/tables/create-tables-database-engine.md).  
  
4.  Haga clic con el botón derecho en la nueva tabla creada anteriormente y, luego, haga clic en **Diseño**.  
  
5.  En el menú **Diseñador de tablas** , haga clic en **Índices o claves**.  
  
6.  En el cuadro de diálogo **Índices o claves** , haga clic en **Agregar**.  
  
7.  Seleccione el nuevo índice en el cuadro de texto **Clave principal o única, o índice seleccionado** .  
  
8.  En la cuadrícula, seleccione **Crear como CLUSTERED**y seleccione **Sí** en la lista desplegable que aparece a la derecha de la propiedad.  
  
9. Haga clic en **Cerrar**.  
  
10. En el menú **Archivo** , haga clic en **Guardar***table_name*.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-create-a-clustered-index"></a>Para crear un índice clúster  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Create a new table with three columns.  
    CREATE TABLE dbo.TestTable  
        (TestCol1 int NOT NULL,  
         TestCol2 nchar(10) NULL,  
         TestCol3 nvarchar(50) NULL);  
    GO  
    -- Create a clustered index called IX_TestTable_TestCol1  
    -- on the dbo.TestTable table using the TestCol1 column.  
    CREATE CLUSTERED INDEX IX_TestTable_TestCol1   
        ON dbo.TestTable (TestCol1);   
    GO  
    ```  
  
 Para obtener más información, vea [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="see-also"></a>Vea también  
 [Crear claves principales](../../relational-databases/tables/create-primary-keys.md)   
 [Crear restricciones UNIQUE](../../relational-databases/tables/create-unique-constraints.md)  
  
  

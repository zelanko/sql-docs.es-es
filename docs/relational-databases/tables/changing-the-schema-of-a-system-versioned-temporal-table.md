---
title: Cambio del esquema de una tabla temporal con control de versiones del sistema | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/28/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9dbe5a21-9335-4f8b-85fd-9da83df79946
caps.latest.revision: 13
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 97eadf63fb8332ef55d8ccb699241a5e5f0e19d0
ms.lasthandoff: 04/11/2017

---
# <a name="changing-the-schema-of-a-system-versioned-temporal-table"></a>Cambiar el esquema de una tabla temporal con control de versiones del sistema
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Use la instrucción **ALTER TABLE** para agregar, modificar o quitar una columna.  
  
## <a name="examples"></a>Ejemplos  
 Estos son algunos ejemplos que cambian el esquema de la tabla temporal.  
  
```  
ALTER TABLE dbo.Department   
   ALTER COLUMN  DeptName varchar(100);   
  
ALTER TABLE dbo.Department   
   ADD WebAddress nvarchar(255) NOT NULL    
   CONSTRAINT DF_WebAddress DEFAULT 'www.mycompany.com';   
  
ALTER TABLE dbo.Department   
   ADD TempColumn INT;   
  
GO   
  
ALTER TABLE dbo.Department   
   DROP COLUMN TempColumn;  
  
/* Setting IsHidden property for period columns.   
Use ALTER COLUMN <period_column> DROP HIDDEN to clear IsHidden flag */  
  
ALTER TABLE dbo.Department   
   ALTER COLUMN SysStartTime ADD HIDDEN;   
  
ALTER TABLE dbo.Department   
   ALTER COLUMN SysEndTime ADD HIDDEN;  
  
```  
  
### <a name="important-remarks"></a>Notas importantes  
  
-   Se requiere el permiso**CONTROL** en tablas de historial y actuales para cambiar el esquema de tabla temporal.  
  
-   Durante una operación **ALTER TABLE** , el sistema mantiene un bloqueo de esquema en ambas tablas.  
  
-   El cambio de esquema especificado se propaga a la tabla de historial de manera adecuada (según el tipo de cambio)  
  
-   Si agrega una columna que no admite valores NULL o modifica una columna existente para que no admita valores NULL, debe especificar el valor predeterminado de las filas existentes. El sistema generará un valor predeterminadas adicional con el mismo valor y lo aplicará a la tabla de historial. Agregar **DEFAULT** a una tabla no vacía es una operación de tamaño de datos en todas las ediciones excepto en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition (donde es una operación de metadatos).  
  
-   Agregar varchar(max), nvarchar(max), varbinary(max) o columnas XML con valores predeterminados será una operación de actualización de datos en todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Si el tamaño de fila tras la adición de columna supera el límite de tamaño de fila, no se pueden agregar nuevas columnas en línea.  
  
-   Una vez que amplía una tabla con una nueva columna que no es NULL, considere la posibilidad de quitar la restricción predeterminada de la tabla de historial, ya que todas las columnas de esa tabla las rellena el sistema automáticamente.  
  
-   La opción en línea (**WITH (ONLINE = ON**) no tiene ningún efecto sobre **ALTER TABLE ALTER COLUMN** en las tablas temporales con versiones del sistema. La columna ALTER no se realiza como en línea, independientemente del valor que se especificó para la opción ONLINE.  
  
-   Puede usar **ALTER COLUMN** para cambiar la propiedad **IsHidden** para las columnas de período.  
  
-   No puede usar **ALTER** directa para los siguientes cambios de esquema. Para estos tipos de cambios, establezca **SYSTEM_VERSIONING = OFF**.  
  
    -   Agregar una columna calculada  
  
    -   Agregar una columna **IDENTITY**  
  
    -   Agregar una columna **SPARSE** o cambiar la columna existente para que sea **SPARSE**si la tabla de historial está establecida en **DATA_COMPRESSION = PAGE** o en **DATA_COMPRESSION = ROW**, que es el valor predeterminado de la tabla de historial.  
  
    -   Agregar un **COLUMN_SET**  
  
    -   Agregar una columna **ROWGUIDCOL** o cambiar una columna existente para que sea **ROWGUIDCOL**  
  
         En el siguiente ejemplo se muestra el cambio del esquema en el que el valor **SYSTEM_VERSIONING = OFF** sigue siendo necesario (agregar columna **IDENTITY** ).   
        Tenga en cuenta que este ejemplo deshabilita la comprobación de coherencia de datos. Esta comprobación no es necesaria si se realiza el cambio de esquema dentro de una transacción en la que no pueden producirse cambios de datos simultáneos.  
  
        ```  
        BEGIN TRAN   
        ALTER TABLE [dbo].[CompanyLocation] SET (SYSTEM_VERSIONING = OFF);   
        ALTER TABLE [CompanyLocation] ADD Cntr INT IDENTITY (1,1);   
        ALTER TABLE [dbo].[CompanyLocationHistory] ADD Cntr INT NOT NULL DEFAULT 0;   
        ALTER TABLE [dbo].[CompanyLocation]    
        SET    
        (   
        SYSTEM_VERSIONING = ON (HISTORY_TABLE = [dbo].[CompanyLocationHistory])   
        );   
        COMMIT ;  
  
        ```  
  
## <a name="did-this-article-help-you-were-listening"></a>¿Le ayudó este artículo? Le escuchamos  
 ¿Qué información está buscando? ¿La encontró? Escuchamos sus comentarios para mejorar el contenido. Envíe sus comentarios a [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Changing%20the%20Schema%20of%20a%20System-Versioned%20Temporal%20Table%20page)  
  
## <a name="see-also"></a>Vea también  
 [Tablas temporales](../../relational-databases/tables/temporal-tables.md)   
 [Introducción a las tablas temporales con versión del sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Administración de la retención de datos históricos en las tablas temporales con versiones del sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Tablas temporales con control de versiones del sistema con tablas con optimización para memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [Creación de una tabla temporal con control de versiones del sistema](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)   
 [Modificación de los datos de una tabla temporal con control de versiones del sistema](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)   
 [Consulta de los datos de una tabla temporal con control de versiones del sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)   
 [Detención del control de versiones en una tabla temporal con control de versiones](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
  


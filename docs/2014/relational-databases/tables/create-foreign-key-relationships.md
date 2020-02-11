---
title: Creación de relaciones de claves externas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- relationships [SQL Server], creating
ms.assetid: 867a54b8-5be4-46e6-9702-49ae6dabf67c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8b5789a277eac84d9753a180b418c05c5fd71d09
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62761612"
---
# <a name="create-foreign-key-relationships"></a>Crear relaciones de clave externa
  En este tema se describe cómo crear relaciones de clave externa en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Cuando se asocian filas de una tabla con filas de otra tabla, se crea una relación entre las dos tablas.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para crear relaciones de clave externa mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   No es necesario que una restricción de clave externa esté vinculada únicamente a una restricción de clave principal de otra tabla; también puede definirse para que haga referencia a las columnas de una restricción UNIQUE de otra tabla.  
  
-   Si se especifica un valor distinto de NULL en la columna de una restricción FOREIGN KEY, el valor debe existir en la columna a que se hace referencia; de lo contrario, se devolverá un error de infracción de clave externa. Para asegurarse de que todos los valores de la restricción de clave externa compuesta se comprueben, especifique NOT NULL en todas las columnas que participan.  
  
-   Las restricciones FOREIGN KEY solo pueden hacer referencia a las tablas de la misma base de datos en el mismo servidor. La integridad referencial entre bases de datos debe implementarse a través de desencadenadores. Para obtener más información, vea [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql).  
  
-   Las restricciones FOREIGN KEY pueden hacer referencia a otras columnas de la misma tabla. Esto recibe el nombre de autorreferencia.  
  
-   Una restricción FOREIGN KEY especificada en el nivel de columna solo puede incluir una columna de referencia. Esta columna debe tener el mismo tipo de datos que la columna en la que se define la restricción.  
  
-   Una restricción FOREIGN KEY especificada en el nivel de tabla debe tener el mismo número de columnas de referencia que la lista de columnas de la restricción. El tipo de datos de cada columna de referencia debe ser también el mismo que el de la columna correspondiente de la lista de columnas.  
  
-   El [!INCLUDE[ssDE](../../includes/ssde-md.md)] no tiene un límite predefinido para el número de restricciones FOREIGN KEY que una tabla que hace referencia a otras tablas puede contener, o para el número de restricciones FOREIGN KEY pertenecientes a otras tablas que hacen referencia a una tabla específica. No obstante, el número real de restricciones FOREIGN KEY que se puede utilizar está limitado por la configuración del hardware y por el diseño de la base de datos y de la aplicación. Se recomienda que la tabla no contenga más de 253 restricciones FOREIGN KEY y que no más de 253 restricciones FOREIGN KEY hagan referencia a ella.  
  
-   Las restricciones FOREIGN KEY no se exigen en tablas temporales.  
  
-   Si la clave externa se define en una columna de tipo definido por el usuario CLR, la implementación del tipo debe admitir el orden binario. Para obtener más información, vea [Tipos definidos por el usuario de CLR](../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
-   Una columna de tipo `varchar(max)` puede participar en una restricción FOREIGN KEY solo si la clave principal a la que hace referencia se define también como tipo `varchar(max)`.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 La creación de una tabla nueva con una clave externa requiere el permiso CREATE TABLE en la base de datos y el permiso ALTER en el esquema en el que se crea la tabla.  
  
 La creación de una clave externa en una tabla existente requiere el permiso ALTER en la tabla.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-create-a-foreign-key-relationship-in-table-designer"></a>Para crear una relación de clave externa en el Diseñador de tablas  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en la tabla que va a estar en el lado de la clave externa de la relación y, después, haga clic en **Diseño**.  
  
     La tabla se abre en el **Diseñador de tablas**.  
  
2.  En el menú **Diseñador de tablas** , haga clic en **Relaciones**.  
  
3.  En el cuadro de diálogo **Relaciones de clave externa**, haga clic en **Agregar**.  
  
     La relación aparece en la lista **relación seleccionada** con un nombre proporcionado por el sistema con el formato FK_\<*TableName*>_\<*TableName*>, donde *TableName* es el nombre de la tabla de clave externa.  
  
4.  Haga clic en la relación en la lista **Relación seleccionada** .  
  
5.  Haga clic en **Especificaciones de tablas y columnas** en la cuadrícula situada a la derecha y, después, haga clic en los puntos suspensivos (**...**) situados a la derecha de la propiedad.  
  
6.  En el cuadro de diálogo **Tablas y columnas** , en la lista desplegable **Clave principal** , elija la tabla que estará en el lado de la clave principal de la relación.  
  
7.  En la cuadrícula situada debajo, elija las columnas que contribuyen a la clave principal de la tabla. En la celda de la cuadrícula adyacente situada a la izquierda de cada columna, elija la columna de clave externa correspondiente de la tabla de clave externa.  
  
     **Diseñador de tablas** sugiere un nombre para la relación. Para cambiar este nombre, edite el contenido del cuadro de texto **Nombre de la relación** .  
  
8.  Elija **Aceptar** para crear la relación.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-create-a-foreign-key-in-a-new-table"></a>Para crear una clave externa en una tabla nueva  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. El ejemplo crea una tabla y definir una restricción de clave externa en la columna `TempID` que hace referencia a la columna `SalesReasonID` de la tabla `Sales.SalesReason` . Las cláusulas ON DELETE CASCADE y ON UPDATE CASCADE se usan para garantizar que los cambios realizados en la tabla `Sales.SalesReason` se propaguen automáticamente a la tabla `Sales.TempSalesReason` .  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE Sales.TempSalesReason (TempID int NOT NULL, Name nvarchar(50),   
    CONSTRAINT PK_TempSales PRIMARY KEY NONCLUSTERED (TempID),   
    CONSTRAINT FK_TempSales_SalesReason FOREIGN KEY (TempID)   
        REFERENCES Sales.SalesReason (SalesReasonID)   
        ON DELETE CASCADE  
        ON UPDATE CASCADE  
    );GO  
  
    ```  
  
#### <a name="to-create-a-foreign-key-in-an-existing-table"></a>Para crear una clave externa de una tabla existente  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. El ejemplo crea una clave externa en la columna `TempID` que hace referencia a la columna `SalesReasonID` de la tabla `Sales.SalesReason`.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Sales.TempSalesReason   
    ADD CONSTRAINT FK_TempSales_SalesReason FOREIGN KEY (TempID)   
        REFERENCES Sales.SalesReason (SalesReasonID)   
        ON DELETE CASCADE  
        ON UPDATE CASCADE  
    ;  
    GO  
  
    ```  
  
     Para obtener más información, vea [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql), [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql) y [table_constraint &#40;Transact-SQL&#41;](/sql/relational-databases/system-information-schema-views/table-constraints-transact-sql).  
  
  

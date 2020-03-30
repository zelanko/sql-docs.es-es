---
title: Creación de relaciones de claves externas | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- relationships [SQL Server], creating
ms.assetid: 867a54b8-5be4-46e6-9702-49ae6dabf67c
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9a26c03eaef6eecf0cee442d2b5b55f599c58065
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68123747"
---
# <a name="create-foreign-key-relationships"></a>Crear relaciones de clave externa

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

En este artículo se describe cómo crear relaciones de clave externa en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Cuando se asocian filas de una tabla con filas de otra tabla, se crea una relación entre las dos tablas.

## <a name="before-you-begin-limits-and-restrictions"></a><a name="BeforeYouBegin"></a> Antes de comenzar Límites y restricciones

- No es necesario que una restricción de clave externa esté vinculada únicamente a una restricción de clave principal de otra tabla; también puede definirse para que haga referencia a las columnas de una restricción UNIQUE de otra tabla.
- Si se especifica un valor distinto de NULL en la columna de una restricción FOREIGN KEY, el valor debe existir en la columna a que se hace referencia; de lo contrario, se devolverá un error de infracción de clave externa. Para asegurarse de que todos los valores de la restricción de clave externa compuesta se comprueben, especifique NOT NULL en todas las columnas que participan.
- Las restricciones FOREIGN KEY solo pueden hacer referencia a las tablas de la misma base de datos en el mismo servidor. La integridad referencial entre bases de datos debe implementarse a través de desencadenadores. Para obtener más información, vea [CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md).
- Las restricciones FOREIGN KEY pueden hacer referencia a otras columnas de la misma tabla. Esto recibe el nombre de autorreferencia.
- Una restricción FOREIGN KEY especificada en el nivel de columna solo puede incluir una columna de referencia. Esta columna debe tener el mismo tipo de datos que la columna en la que se define la restricción.
- Una restricción FOREIGN KEY especificada en el nivel de tabla debe tener el mismo número de columnas de referencia que la lista de columnas de la restricción. El tipo de datos de cada columna de referencia debe ser también el mismo que el de la columna correspondiente de la lista de columnas.
- El [!INCLUDE[ssDE](../../includes/ssde-md.md)] no tiene un límite predefinido para el número de restricciones FOREIGN KEY que una tabla que hace referencia a otras tablas puede contener, o para el número de restricciones FOREIGN KEY pertenecientes a otras tablas que hacen referencia a una tabla específica. No obstante, el número real de restricciones FOREIGN KEY que se puede utilizar está limitado por la configuración del hardware y por el diseño de la base de datos y de la aplicación. Una tabla puede hacer referencia a otras 253 tablas y columnas como claves externas (referencias de salida) como máximo. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] aumenta el límite para la cantidad de otras tablas y columnas que pueden hacer referencia a las columnas de una sola tabla (referencias de entrada) de 253 a 10 000. (Requiere al menos el nivel de compatibilidad 130). El aumento conlleva las siguientes restricciones:

  - Se admiten más de 253 referencias de clave externa para las operaciones DELETE y UPDATE DML. Las operaciones MERGE no se admiten.
  - Una tabla con una referencia de clave externa a sí misma seguirá limitada a 253 referencias de clave externa.
  - Actualmente, no hay disponibles más de 253 referencias de clave externa para índices de almacén de columnas, tablas optimizadas para memoria o Stretch Database.

- Las restricciones FOREIGN KEY no se exigen en tablas temporales.
- Si la clave externa se define en una columna de tipo definido por el usuario CLR, la implementación del tipo debe admitir el orden binario. Para obtener más información, vea [Tipos definidos por el usuario de CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).
- Una columna de tipo **varchar(max)** solo puede participar en una restricción FOREIGN KEY si la clave principal a la que hace referencia se define también como tipo **varchar(max)** .

## <a name="permissions"></a>Permisos

La creación de una tabla nueva con una clave externa requiere el permiso CREATE TABLE en la base de datos y el permiso ALTER en el esquema en el que se crea la tabla.

La creación de una clave externa en una tabla existente requiere el permiso ALTER en la tabla.

## <a name="create-a-foreign-key-relationship-in-table-designer"></a>Crear una relación de clave externa en el Diseñador de tablas

### <a name="using-sql-server-management-studio"></a>Uso de SQL Server Management Studio

1. En el Explorador de objetos, haga clic con el botón derecho en la tabla que va a estar en el lado de la clave externa de la relación y, después, haga clic en **Diseño**.

   La tabla se abre en el **Diseñador de tablas**.
2. En el menú **Diseñador de tablas** , haga clic en **Relaciones**.
3. En el cuadro de diálogo **Relaciones de clave externa** , haga clic en **Agregar**.

   La relación aparece en la lista **Relación seleccionada** con un nombre proporcionado por el sistema con el formato FK_\<*tablename*>_\<*tablename*>, donde *tablename* es el nombre de la tabla de clave externa.
4. Haga clic en la relación en la lista **Relación seleccionada** .
5. Haga clic en **Especificaciones de tablas y columnas** en la cuadrícula situada a la derecha y, después, haga clic en los puntos suspensivos ( **...** ) situados a la derecha de la propiedad.
6. En el cuadro de diálogo **Tablas y columnas** , en la lista desplegable **Clave principal** , elija la tabla que estará en el lado de la clave principal de la relación.
7. En la cuadrícula situada debajo, elija las columnas que contribuyen a la clave principal de la tabla. En la celda de la cuadrícula adyacente situada a la izquierda de cada columna, elija la columna de clave externa correspondiente de la tabla de clave externa.

   El**Diseñador de tablas** sugerirá un nombre para la relación. Para cambiar este nombre, edite el contenido del cuadro de texto **Nombre de la relación** .
8. Elija **Aceptar** para crear la relación.

## <a name="create-a-foreign-key-in-a-new-table"></a>Crear una clave externa en una tabla nueva

### <a name="using-transact-sql"></a>Usar Transact-SQL

En el ejemplo siguiente se crea una tabla y se define una restricción de clave externa en la columna `TempID` que hace referencia a la columna `SalesReasonID` de la tabla `Sales.SalesReason` en la base de datos de AdventureWorks. Las cláusulas ON DELETE CASCADE y ON UPDATE CASCADE se usan para garantizar que los cambios realizados en la tabla `Sales.SalesReason` se propaguen automáticamente a la tabla `Sales.TempSalesReason` .    

```sql
CREATE TABLE Sales.TempSalesReason 
   (
      TempID int NOT NULL, Name nvarchar(50)
      , CONSTRAINT PK_TempSales PRIMARY KEY NONCLUSTERED (TempID)
      , CONSTRAINT FK_TempSales_SalesReason FOREIGN KEY (TempID)
        REFERENCES Sales.SalesReason (SalesReasonID)
        ON DELETE CASCADE
        ON UPDATE CASCADE
   )
;
```

## <a name="create-a-foreign-key-in-an-existing-table"></a>Crear una clave externa de una tabla existente

### <a name="using-transact-sql"></a>Usar Transact-SQL
En el ejemplo siguiente crea una clave externa en la columna `TempID` y hace referencia a la columna `SalesReasonID` de la tabla `Sales.SalesReason` de la base de datos de AdventureWorks.

```sql
ALTER TABLE Sales.TempSalesReason
   ADD CONSTRAINT FK_TempSales_SalesReason FOREIGN KEY (TempID)
      REFERENCES Sales.SalesReason (SalesReasonID)
      ON DELETE CASCADE
      ON UPDATE CASCADE
;
```
Para más información, consulte:

- [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)
- [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)
- [table_constraint](../../t-sql/statements/alter-table-table-constraint-transact-sql.md).

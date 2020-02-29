---
title: Creación de tablas (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table creation [SQL Server], Visual Database Tools
ms.assetid: 6f7c6ac5-e6d3-4dca-831e-b28442ba535b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 261aab8b0e8a5d80aed143d6b29e952243742917
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176825"
---
# <a name="create-tables-database-engine"></a>Crear tablas (motor de base de datos)
  Puede crear una nueva tabla, asignarle un nombre y agregarla a una base de datos existente en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].

> [!NOTE]
>  Si está conectado a una base de datos de SQL Azure, la opción de nueva tabla inicia un script de plantilla de creación de tabla. Modifique los parámetros y, a continuación, ejecute el script para crear una nueva tabla. Para obtener más información, vea [Introducción a SQL Azure](https://microsoft.sharepoint.com/sites/infopedia_g01/pages/cards/azure-sql-database.aspx).

 **En este tema**

-   **Antes de empezar:**

     [Seguridad](#Security)

-   **Para crear una tabla con:**

     [SQL Server Management Studio](#SSMSProcedure)

     [Transact-SQL](#TsqlProcedure)

##  <a name="BeforeYouBegin"></a> Antes de comenzar

###  <a name="Security"></a> Seguridad

####  <a name="Permissions"></a> Permisos
 Se necesita el permiso CREATE TABLE en la base de datos y el permiso ALTER en el esquema en que se crea la tabla.

 Si alguna columna de la instrucción CREATE TABLE se define como un tipo definido por el usuario de CLR, se necesita la propiedad del tipo o el permiso REFERENCES.

 Si las columnas de la instrucción CREATE TABLE tienen asociada una colección de esquemas XML, se necesita la propiedad de la colección de esquemas XML o el permiso REFERENCES.

##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio

#### <a name="to-create-a-table-with-table-designer"></a>Para crear una tabla con el Diseñador de tablas

1.  En el **Explorador de objetos**, conéctese a la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] que contiene la base de datos que se va a modificar.

2.  En el **Explorador de objetos**, expanda el nodo **Bases de datos** y, a continuación, expanda la base de datos que contendrá la nueva tabla.

3.  En el Explorador de objetos, haga clic con el botón derecho en el nodo **Tablas** de la base de datos y, después, haga clic en **Nueva tabla**.

4.  Escriba los nombres de columna, elija los tipos de datos y elija si desea permitir valores NULL para cada columna como se muestra en la ilustración siguiente.

     ![AddColumnsinTableDesigner](../../database-engine/media/addcolumnsintabledesigner.gif "AddColumnsinTableDesigner")

5.  Para especificar más propiedades para una columna, como la identidad o valores de columna calculada, haga clic en la columna y después, en la pestaña de propiedades de la columna, elija las propiedades adecuadas. Para obtener más información sobre las propiedades de columna, vea [Propiedades de columnas de tablas &#40;SQL Server Management Studio&#41;](table-column-properties-sql-server-management-studio.md).

6.  Para especificar una columna como clave principal, haga clic con el botón derecho en la columna y seleccione **Establecer clave principal**. Para obtener más información, consulte [Create Primary Keys](../tables/create-primary-keys.md).

7.  Para crear relaciones de clave externa, restricciones CHECK o índices, haga clic con el botón secundario en el panel Diseñador de tablas y seleccione un objeto de la lista como se muestra en la ilustración siguiente.

     ![AddTableObjects](../../database-engine/media/addtableobjects.gif "AddTableObjects")

     Para obtener más información acerca de estos objetos, vea [Create Foreign Key Relationships](../tables/create-foreign-key-relationships.md), [Create Check Constraints](../tables/create-check-constraints.md) e [Indexes](../indexes/indexes.md).

8.  De forma predeterminada, la tabla está contenida en el esquema **dbo** . Para especificar un esquema diferente para la tabla, haga clic con el botón derecho en el panel Diseñador de tablas y seleccione **Propiedades** como se muestra en la ilustración siguiente. En la lista desplegable **Esquema** , seleccione el esquema adecuado.

     ![Specifyatableschema](../../database-engine/media/specifyatableschema.gif "Specifyatableschema")

     Para obtener más información acerca de los esquemas, vea [Create a Database Schema](../security/authentication-access/create-a-database-schema.md).

9. En el menú **archivo** , elija **Guardar** *nombre de tabla*.

10. En el cuadro de diálogo **Elegir nombre** , escriba un nombre para la tabla y haga clic en **Aceptar**.

11. Para ver la nueva tabla, en el **Explorador de objetos**, expanda el nodo **Tablas** y presione **F5** para actualizar la lista de objetos. La nueva tabla se mostrará en la lista de tablas.

##  <a name="TsqlProcedure"></a> Usar Transact-SQL

#### <a name="to-create-a-table-in-the-query-editor"></a>Para crear una tabla en el Editor de consultas

1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].

2.  En la barra de Estándar, haga clic en **Nueva consulta**.

3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.

    ```
    CREATE TABLE dbo.PurchaseOrderDetail
    (
        PurchaseOrderID int NOT NULL
        ,LineNumber smallint NOT NULL
        ,ProductID int NULL
        ,UnitPrice money NULL
        ,OrderQty smallint NULL
        ,ReceivedQty float NULL
        ,RejectedQty float NULL
        ,DueDate datetime NULL
    );
    ```

 Para obtener más ejemplos, vea [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql).



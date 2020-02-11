---
title: Ver funciones definidas por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.udfproperties.general.f1
- sql12.swb.functionproperties.general.f1
helpviewer_keywords:
- displaying user-defined functions
- viewing user-defined functions
- user-defined functions [SQL Server], viewing
- status information [SQL Server], user-defined functions
ms.assetid: a45dfab5-6384-4311-b935-2e23a70c5c10
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ea37fdca56c222cbebbdcb00956938a92fe2c203
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211683"
---
# <a name="view-user-defined-functions"></a>Ver funciones definidas por el usuario
  Puede obtener información sobre la definición o las propiedades de una función definida por el usuario en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Es posible que necesite ver la definición de la función para entender cómo se derivan sus datos de las tablas de origen o para ver los datos que ella misma define.  
  
> [!IMPORTANT]  
>  Si cambia el nombre de un objeto al que hace referencia una función, deberá modificar esa función para que el texto refleje el nuevo nombre. Por tanto, antes de cambiar el nombre de un objeto, muestre primero las dependencias del objeto para determinar si alguna función va a verse afectada por el cambio propuesto.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para obtener información acerca de una función, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 El uso de **sys.sql_expression_dependencies** para buscar todas las dependencias de una función necesita el permiso VIEW DEFINITION en la base de datos y el permiso SELECT en **sys.sql_expression_dependencies** para la base de datos. Las definiciones de objetos del sistema, como las que se devuelven en OBJECT_DEFINITION, son visibles de forma pública.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-show-a-user-defined-functions-properties"></a>Para mostrar las propiedades de una función definida por el usuario  
  
1.  En el **Explorador de objetos**, haga clic en el signo más situado junto a la base de datos que contiene la función cuyas propiedades desea ver y haga clic en el signo más para expandir la carpeta **Programación** .  
  
2.  Haga clic en el signo más para expandir la carpeta **Funciones** .  
  
3.  Haga clic en el signo más para expandir la carpeta que contiene la función cuyas propiedades desea ver:  
  
    -   Table-valued Function  
  
    -   Función con valor escalar  
  
    -   Función de agregado  
  
4.  Haga clic con el botón derecho en la función cuyas propiedades quiere ver y seleccione **Propiedades**.  
  
     Las propiedades siguientes aparecen en el cuadro de diálogo **Propiedades de la función:** _nombre_función_.  
  
     **Base de datos**  
     Nombre de la base de datos que contiene esta función.  
  
     **Server**  
     Nombre de la instancia de servidor actual.  
  
     **User**  
     Nombre del usuario de esta conexión.  
  
     **Fecha de creación**  
     Muestra la fecha de creación de la función.  
  
     **Ejecutar como**  
     Contexto de ejecución para la función.  
  
     **Nombre**  
     Nombre de la función actual.  
  
     **Esquema**  
     Muestra el esquema al que pertenece la función.  
  
     **Objeto de sistema**  
     Indica si la función es un objeto de sistema. Los valores son True y False.  
  
     **Valores NULL ANSI**  
     Indica si el objeto se ha creado con la opción Valores NULL ANSI.  
  
     **Cifrado**  
     Indica si la función está cifrada. Los valores son True y False.  
  
     **Tipo de función**  
     Tipo de la función definida por el usuario.  
  
     **Identificador entre comillas**  
     Indica si el objeto se ha creado con la opción Identificador entre comillas.  
  
     **Enlazado a esquema**  
     Indica si la función está enlazada a un esquema. Los valores son True y False. Para obtener más información sobre las funciones enlazadas a esquema, vea la sección SCHEMABINDING de [CREATE FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql).  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-get-the-definition-and-properties-of-a-function"></a>Para obtener la definición y propiedades de una función  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue uno de los ejemplos siguientes en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get the function name, definition, and relevant properties  
    SELECT sm.object_id,   
       OBJECT_NAME(sm.object_id) AS object_name,   
       o.type,   
       o.type_desc,   
       sm.definition,  
       sm.uses_ansi_nulls,  
       sm.uses_quoted_identifier,  
       sm.is_schema_bound,  
       sm.execute_as_principal_id  
    -- using the two system tables sys.sql_modules and sys.objects  
    FROM sys.sql_modules AS sm  
    JOIN sys.objects AS o ON sm.object_id = o.object_id  
    -- from the function 'dbo.ufnGetProductDealerPrice'  
    WHERE sm.object_id = OBJECT_ID('dbo.ufnGetProductDealerPrice')  
    ORDER BY o.type;  
    GO  
  
    ```  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get the definition of the function dbo.ufnGetProductDealerPrice  
    SELECT OBJECT_DEFINITION (OBJECT_ID('dbo.ufnGetProductDealerPrice')) AS ObjectDefinition;  
    GO  
    ```  
  
 Para obtener más información, vea [sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql) y [OBJECT_DEFINITION &#40;Transact-SQL&#41;](/sql/t-sql/functions/object-definition-transact-sql).  
  
#### <a name="to-get-the-dependencies-of-a-function"></a>Para obtener las dependencias de una función  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get all of the dependency information  
    SELECT OBJECT_NAME(sed.referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(sed.referencing_id, sed.referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        sed.referencing_class_desc, sed.referenced_class_desc,  
        sed.referenced_server_name, sed.referenced_database_name, sed.referenced_schema_name,  
        sed.referenced_entity_name,   
        COALESCE(COL_NAME(sed.referenced_id, sed.referenced_minor_id), '(n/a)') AS referenced_column_name,  
        sed.is_caller_dependent, sed.is_ambiguous  
    -- from the two system tables sys.sql_expression_dependencies and sys.object  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    -- on the function dbo.ufnGetProductDealerPrice  
    WHERE sed.referencing_id = OBJECT_ID('dbo.ufnGetProductDealerPrice');  
    GO  
    ```  
  
 Para obtener más información, vea [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql) y [sys.objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-objects-transact-sql).  
  
  

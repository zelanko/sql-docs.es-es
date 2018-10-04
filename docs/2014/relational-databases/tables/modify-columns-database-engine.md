---
title: Modificación de columnas (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- modifying data types
- column data types [SQL Server]
- data types [SQL Server], columns
ms.assetid: b67b95c5-61ef-4bd8-9a3e-1640eb7583ac
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4d98b8de8e4ced15291684ba304bfd04c6c62b7c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48161165"
---
# <a name="modify-columns-database-engine"></a>Modificar columnas (motor de base de datos)
  En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , el tipo de datos de una columna se puede modificar mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!WARNING]  
>  Al modificar el tipo de datos de una columna que ya contiene datos, estos datos se pueden perder definitivamente cuando los datos existentes se convierten al nuevo tipo. Se pueden producir además errores en el código y las aplicaciones que dependen de la columna modificada. Los elementos afectados pueden ser consultas, vistas, procedimientos almacenados, funciones definidas por el usuario y aplicaciones cliente. Tenga en cuenta que estos errores se producirán en cascada. Por ejemplo, puede producirse un error en un procedimiento almacenado que llama a una función definida por el usuario que, a su vez, depende de la columna modificada. Tenga en cuenta las consecuencias antes de realizar cualquier cambio en una columna.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para modificar el tipo de datos de una columna con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-modify-the-data-type-of-a-column"></a>Para modificar el tipo de datos de una columna  
  
1.  En el **Explorador de objetos**, haga clic con el botón derecho en la tabla que contenga columnas cuya escala quiera cambiar y, después, haga clic en **Diseño**.  
  
2.  Seleccione la columna en la que desea modificar el tipo de datos.  
  
3.  En la pestaña **Propiedades de columna** , haga clic en la celda de la cuadrícula de la propiedad **Tipo de datos** y elija un tipo de datos en la lista desplegable.  
  
4.  En el menú **Archivo**, haga clic en **Guardar***nombre de tabla*.  
  
> [!NOTE]  
>  Cuando se modifica el tipo de datos de una columna, el Diseñador de tablas aplica la longitud del tipo de datos predeterminada que se ha seleccionado, aunque ya se haya especificado otra. Defina siempre la longitud del tipo de datos del valor deseado después de especificar el tipo de datos.  
  
> [!WARNING]  
>  Si intenta modificar el tipo de datos de una columna relacionada con otras tablas, el Diseñador de tablas le pide que confirme que el cambio tenga que realizarse también en las columnas de otras tablas.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-modify-the-data-type-of-a-column"></a>Para modificar el tipo de datos de una columna  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    CREATE TABLE dbo.doc_exy (column_a INT ) ;  
    GO  
    INSERT INTO dbo.doc_exy (column_a) VALUES (10) ;  
    GO  
    ALTER TABLE dbo.doc_exy ALTER COLUMN column_a DECIMAL (5, 2) ;  
    GO  
  
    ```  
  
 Para obtener más información, vea [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
  

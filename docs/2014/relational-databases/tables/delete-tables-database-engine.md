---
title: Eliminación de tablas (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table deletions [SQL Server]
- deleting tables
- removing tables
- dropping tables
ms.assetid: ca6aa3e9-9885-44c3-bafc-aec441fd97ec
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f040c9907574bba718827999bb9c0fbb432a0bd0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62761434"
---
# <a name="delete-tables-database-engine"></a>Eliminar tablas (motor de base de datos)
  Puede eliminar (quitar) una tabla de la base de datos de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!CAUTION]  
>  Piénselo bien antes de eliminar una tabla. Si las consultas, las vistas, las funciones definidas por el usuario, los procedimientos almacenados o los programas existentes hacen referencia a la tabla, la eliminación de la tabla hará que estos objetos dejen de ser válidos.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para eliminar una tabla con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   No se puede eliminar una tabla a la que haga referencia una restricción FOREIGN KEY. Primero se debe quitar la restricción FOREIGN KEY o la tabla de referencia. Si la tabla de referencia y la tabla que tiene la clave principal se van a quitar en la misma instrucción DROP TABLE, la tabla de referencia debe aparecer primero.  
  
-   Cuando se quita la tabla, las reglas o valores predeterminados de la tabla pierden sus enlaces y se quitan automáticamente las restricciones o desencadenadores asociados con la tabla. Si vuelve a crear una tabla, debe volver a enlazar las reglas y valores predeterminados apropiados, volver a crear los desencadenadores y agregar todas las restricciones necesarias.  
  
-   Si quita una tabla que contiene una columna `varbinary (max)` con el atributo FILESTREAM, los datos almacenados en el sistema de archivos no se quitarán.  
  
-   DROP TABLE y CREATE TABLE no se deberían ejecutar en la misma tabla en el mismo lote. De lo contrario, podría producirse un error inesperado.  
  
-   Las vistas o procedimientos almacenados que hagan referencia a la tabla quitada se deben eliminar o modificar explícitamente para quitar la referencia a la tabla.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Se requiere el permiso ALTER en el esquema al que pertenece la tabla, el permiso CONTROL en la tabla o la pertenencia al rol fijo de base de datos **db_ddladmin** .  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-delete-a-table-from-the-database"></a>Para eliminar una tabla de la base de datos  
  
1.  En el Explorador de objetos, seleccione la tabla que desea eliminar.  
  
2.  Haga clic con el botón derecho en la tabla y elija **Eliminar** en el menú contextual.  
  
3.  Un cuadro de mensaje le pedirá que confirme la eliminación. Haga clic en **Sí**.  
  
    > [!NOTE]  
    >  Al eliminar una tabla, se suprimirán automáticamente todas relaciones que mantenga.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-delete-a-table-in-query-editor"></a>Para eliminar una tabla en el Editor de consultas  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    DROP TABLE dbo.PurchaseOrderDetail;  
  
    ```  
  
 Para obtener más información, vea [DROP TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-table-transact-sql).  
  
  

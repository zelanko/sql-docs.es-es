---
title: Cambio de nombre de las funciones definidas por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: c2695a5c-9cc5-4b18-8771-53027ca9a9af
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3419faca26d9d252610c07cb994ab5faa738f937
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211701"
---
# <a name="rename-user-defined-functions"></a>Cambiar el nombre de las funciones definidas por el usuario
  Puede cambiar el nombre de las funciones definidas por el usuario en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para cambiar el nombre de las funciones definidas por el usuario, con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Los nombres de las funciones deben ajustarse a las reglas de los [identificadores](../databases/database-identifiers.md).  
  
-   Al cambiar el nombre de una función definida por el usuario no se cambiará el nombre del objeto correspondiente en la columna de definición de la vista de catálogo **sys.sql_modules** . Por tanto, se recomienda no cambiar este tipo de objeto. En su lugar, quite el procedimiento almacenado y vuelva a crearlo con su nuevo nombre.  
  
-   El hecho de cambiar el nombre o la definición de una función definida por el usuario puede provocar errores en los objetos dependientes si no se actualizan con arreglo a los cambios realizados en la función.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Para quitar la función, se requiere el permiso ALTER en el esquema al que pertenece la función o un permiso CONTROL en la función. Para volver a crear la función, se requiere el permiso CREATE FUNCTION en la base de datos y el permiso ALTER en el esquema en el que se va a crear la función.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-rename-user-defined-functions"></a>Para cambiar el nombre de las funciones definidas por el usuario  
  
1.  En el **Explorador de objetos**, haga clic en el signo más situado junto a la base de datos que contiene la función a la que desea cambiar el nombre y  
  
2.  Haga clic en el signo más junto a la carpeta **Programación** .  
  
3.  Haga clic en el signo más junto a la carpeta que contenga la función cuyo nombre desea cambiar:  
  
    -   Table-valued Function  
  
    -   Función con valor escalar  
  
    -   Función de agregado  
  
4.  Haga clic con el botón derecho en la función cuyo nombre quiere cambiar y seleccione **Cambiar nombre**.  
  
5.  Escriba el nuevo nombre de la función.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para cambiar el nombre de las funciones definidas por el usuario**  
  
 Esta tarea no se puede realizar mediante instrucciones Transact-SQL. Para cambiar una función definida por el usuario mediante Transact-SQL, debe eliminar la función existente y volver a crearla con el nuevo nombre. Asegúrese de que todo el código y las aplicaciones que usaban el nombre antiguo de la función usan el nuevo.  
  
 Para obtener más información, vea [CREATE FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql) y [DROP FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-function-transact-sql).  
  
## <a name="see-also"></a>Vea también  
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)   
 [Ver funciones definidas por el usuario](user-defined-functions.md)  
  
  

---
title: Usar sinónimos (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- synonyms [SQL Server], about synonyms
ms.assetid: 6210e1d5-075f-47e4-ac8d-f84bcf26fbc0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2066eeb7d9b86228ed86aed290e69f2a0e981b95
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62736245"
---
# <a name="synonyms-database-engine"></a>Usar sinónimos (motor de base de datos)
  Un sinónimo es un objeto de base de datos que sirve para los siguientes objetivos:  
  
-   Proporciona un nombre alternativo para otro objeto de base de datos, denominado objeto base, que puede existir en un servidor local o remoto.  
  
-   Proporciona una capa de abstracción que protege una aplicación cliente de cambios realizados en el nombre o la ubicación del objeto base.  
  
 Por ejemplo, suponga la tabla **Employee** de [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)], situada en un servidor denominado **Server1**. Para hacer referencia a esta tabla desde otro servidor, **Server2**, una aplicación cliente tendría que usar el nombre de cuatro partes **Server1.AdventureWorks.Person.Employee**. Además, si la ubicación de la tabla cambiara, por ejemplo a otro servidor, la aplicación cliente debería modificarse para reflejar ese cambio.  
  
 Para solucionar ambas cosas, puede crear un sinónimo, **EmpTable**, en **Server2** para la tabla **Employee** en **Server1**. Ahora la aplicación cliente solo tiene que usar el nombre de una parte, **EmpTable**, para hacer referencia a la tabla **Employee** . Además, si la ubicación de la tabla **Employee** cambia, tendrá que modificar el sinónimo, **EmpTable**, para que apunte a la nueva ubicación de la tabla **Employee** . Puesto que no hay ninguna instrucción ALTER SYNONYM, primero tiene que quitar el sinónimo, **EmpTable**y, luego, volver a crearlo con el mismo nombre, pero apuntando a la nueva ubicación de **Employee**.  
  
 Un sinónimo pertenece a un esquema y, al igual que otros objetos de un esquema, el nombre de un sinónimo debe ser único. Puede crear sinónimos para los siguientes objetos de base de datos:  
  
|||  
|-|-|  
|Procedimiento almacenado del ensamblado (CLR)|Función con valores de tabla del ensamblado (CLR)|  
|Función escalar del ensamblado (CLR)|Función de agregado del ensamblado (CLR)|  
|Procedimiento de filtro de replicación|Procedimiento almacenado extendido|  
|Función escalar de SQL|Función con valores de tabla de SQL|  
|Función SQL insertada con valores de tabla|Procedimiento almacenado de SQL|  
|Ver|Tabla<sup>1</sup> (definida por el usuario)|  
  
 <sup>1</sup> incluye tablas temporales locales y globales  
  
> [!NOTE]  
>  No pueden usarse nombres de cuatro partes para objetos base de función.  
  
 Un sinónimo no puede ser el objeto base de otro sinónimo y un sinónimo no puede hacer referencia a una función de agregado definida por el usuario.  
  
 El enlace entre un sinónimo y su objeto base solo es mediante el nombre. Todas las comprobaciones de existencia, tipo y permisos en el objeto base se posponen hasta la ejecución. Por tanto, el objeto base puede modificarse, quitarse o quitarse y reemplazarse por otro objeto con el mismo nombre que el objeto base original. Por ejemplo, suponga un sinónimo, **MyContacts**, que hace referencia a la tabla **Person.Contact** de [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]. Si la tabla **Contact** se quita y reemplaza por una vista llamada **Person.Contact**, **MyContacts** ahora hace referencia a la vista **Person.Contact** .  
  
 Las referencias a sinónimos no están enlazadas a esquema. Por tanto, un sinónimo puede quitarse en cualquier momento. Sin embargo, al quitar un sinónimo se corre el riesgo de dejar referencias pendientes al sinónimo quitado. Estas referencias solo se encontrarán en tiempo de ejecución.  
  
## <a name="synonyms-and-schemas"></a>Sinónimos y esquemas  
 Si tiene un esquema predeterminado que no posee y desea crear un sinónimo, debe calificar el nombre del sinónimo con el nombre de un esquema que posea. Por ejemplo, si posee un esquema **x**, pero **y** es su esquema predeterminado y usa la instrucción CREATE SYNONYM, debe poner un prefijo al nombre del sinónimo con el esquema **x**, en lugar de asignar un nombre al sinónimo mediante un nombre con una sola parte. Para obtener más información sobre cómo crear sinónimos, vea [CREATE SYNONYM &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-synonym-transact-sql).  
  
## <a name="granting-permissions-on-a-synonym"></a>Conceder permisos para un sinónimo  
 Solo los propietarios de los sinónimos, miembros de **db_owner**o miembros de **db_ddladmin** pueden conceder permiso para un sinónimo.  
  
 Puede conceder (GRANT), denegar (DENY) o revocar (REVOKE) todos o cualquiera de los siguientes permisos para un sinónimo:  
  
|||  
|-|-|  
|CONTROL|SUPRIMIR|  
|Ejecute|INSERT|  
|SELECT|TAKE OWNERSHIP|  
|UPDATE|VIEW DEFINITION|  
  
## <a name="using-synonyms"></a>Usar sinónimos  
 Puede usar sinónimos en lugar de los objetos base a los que se hace referencia en varias instrucciones SQL y contextos de expresión. La siguiente tabla contiene una lista de estas instrucciones y contextos de expresiones:  
  
|||  
|-|-|  
|SELECT|INSERT|  
|UPDATE|SUPRIMIR|  
|Ejecute|Subselecciones|  
  
 Al trabajar con sinónimos en los contextos indicados anteriormente, el objeto base se ve afectado. Por ejemplo, si un sinónimo hace referencia a un objeto base que es una tabla e inserta una fila en el sinónimo, realmente está insertando una fila en la tabla a la que se hace referencia.  
  
> [!NOTE]  
>  No se puede hacer referencia a un sinónimo situado en un servidor vinculado.  
  
 Puede usar un sinónimo como parámetro para la función OBJECT_ID; sin embargo, la función devuelve el identificador de objeto del sinónimo y no el objeto base.  
  
 No puede hacer referencia a un sinónimo en una instrucción DDL. Por ejemplo, las instrucciones siguientes, que hacen referencia a un sinónimo denominado `dbo.MyProduct`, generan errores:  
  
```  
ALTER TABLE dbo.MyProduct  
   ADD NewFlag int null;  
EXEC ('ALTER TABLE dbo.MyProduct  
   ADD NewFlag int null');  
```  
  
 Las siguientes instrucciones de permisos solo están asociadas al sinónimo, no al objeto base:  
  
|||  
|-|-|  
|GRANT|DENY|  
|REVOKE||  
  
 Los sinónimos no están enlazados al esquema, por lo que los siguientes contextos de expresión enlazados al esquema no pueden hacer referencia a sinónimos:  
  
|||  
|-|-|  
|CHECK, restricciones|Columnas calculadas|  
|Expresiones predeterminadas|Expresiones de reglas|  
|Vistas enlazadas a esquema|Funciones enlazadas a esquema|  
  
 Para obtener más información sobre las funciones enlazadas a esquema, vea [Crear funciones definidas por el usuario &#40;motor de base de datos&#41;](../user-defined-functions/create-user-defined-functions-database-engine.md).  
  
## <a name="getting-information-about-synonyms"></a>Obtener información acerca de sinónimos  
 La vista de catálogo sys.synonyms contiene una entrada para cada sinónimo de una base de datos determinada. Esta vista de catálogo expone metadatos de sinónimos, como el nombre del sinónimo y el nombre del objeto base. Para obtener más información sobre la `sys.synonyms` vista de catálogo, vea [sys.synonyms &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-synonyms-transact-sql).  
  
 Mediante las propiedades extendidas, puede agregar texto descriptivo o instrucciones, máscaras de entrada y reglas de formato como propiedades de un sinónimo. Puesto que la propiedad se almacena en la base de datos, todas las aplicaciones que leen la propiedad pueden evaluar el objeto de la misma manera. Para obtener más información, vea [sp_addextendedproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql).  
  
 Para buscar el tipo base del objeto base de un sinónimo, utilice la función OBJECTPROPERTYEX. Para obtener más información, vea [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql).  
  
### <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se devuelve el tipo base del objeto base de un sinónimo; el objeto base es un objeto local.  
  
```  
USE tempdb;  
GO  
CREATE SYNONYM MyEmployee   
FOR AdventureWorks2012.HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('MyEmployee'), 'BaseType') AS BaseType;  
```  
  
 En el siguiente ejemplo se devuelve el tipo base del objeto base de un sinónimo; el objeto base es un objeto remoto ubicado en un servidor llamado `Server1`.  
  
```  
EXECUTE sp_addlinkedserver Server1;  
GO  
CREATE SYNONYM MyRemoteEmployee  
FOR Server1.AdventureWorks2012.HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('MyRemoteEmployee'), 'BaseType') AS BaseType;  
GO  
```  
  
## <a name="related-content"></a>Contenido relacionado  
 [Crear sinónimos](create-synonyms.md)  
  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-synonym-transact-sql)  
  
 [DROP SYNONYM &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-synonym-transact-sql)  
  
  

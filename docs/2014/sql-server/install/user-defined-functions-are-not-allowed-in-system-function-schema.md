---
title: No se permiten funciones definidas por el usuario en system_function_schema | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- system functions [SQL Server]
- user-defined functions [SQL Server], system
ms.assetid: 3cb54053-ef65-4558-ae96-8686b6b22f4f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 10813b7bc0a97f0ba8a81f3f48447142659cd596
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66091332"
---
# <a name="user-defined-functions-are-not-allowed-in-systemfunctionschema"></a>Las funciones definidas por el usuario no se permiten en system_function_schema
  El Asesor de actualizaciones detectó funciones definidas por el usuario que son propiedad del usuario no documentado **system_function_schema**. No puede crear una función del sistema definida por el usuario especificando este usuario. El **system_function_schema** no existe el nombre de usuario y el identificador de usuario que está asociado con este nombre (UID = 4) está reservado para el **sys** esquema y se restringe a solo para uso interno.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 El almacenamiento de objetos del sistema y el acceso han cambiado de las siguientes maneras:  
  
-   Los objetos del sistema se almacenan en solo lectura **recursos** directa no se permiten las actualizaciones de objeto del sistema y base de datos.  
  
     Los objetos del sistema aparecen lógicamente en el **sys** esquema de cada base de datos. Esto mantiene la capacidad de invocar funciones del sistema desde cualquier base de datos especificando un nombre de función con una sola parte. Por ejemplo, la instrucción `SELECT * FROM fn_helpcollations()` se puede ejecutar desde cualquier base de datos.  
  
-   El usuario no documentado **system_function_schema** se ha quitado.  
  
-   El usuario ID asociado con **system_function_schema** (UID = 4) está reservado para el **sys** esquema y se restringe a solo para uso interno.  
  
 Estos cambios tienen el efecto siguiente sobre las funciones del sistema definidas por el usuario:  
  
-   Instrucciones de Definition Language (DDL) de datos que hacen referencia **system_function_schema** se producirá un error. Por ejemplo, la instrucción `CREATE FUNCTION system`_`function` \_ `schema.fn` \_ `MySystemFunction` ... no tendrá éxito.  
  
-   Después de actualizar a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], los objetos existentes que pertenecen a **system_function_schema** solo están contenidos en el **sys** esquema de la **maestro** base de datos. Dado que no se puede modificar los objetos del sistema, estas funciones nunca se pueden modificar o quitar de la **maestro** base de datos. Además, estas funciones no se pueden invocar desde otras bases de datos especificando solo un nombre de función con una parte.  
  
## <a name="corrective-action"></a>Acción correctora  
 Antes de actualizar, lleve a cabo las siguientes tareas:  
  
1.  Cambiar la propiedad de las funciones definidas por el usuario existentes a **dbo** utilizando el **sp_changeobjectowner** procedimiento almacenado del sistema.  
  
2.  Considere cambiar el nombre de la función para que no utilice el prefijo 'fn_'. Esto evitará conflictos potenciales del nombre con otras funciones del sistema existentes o futuras.  
  
3.  Agregue una copia de las funciones modificadas en cada base de datos que las utilice.  
  
4.  Reemplace las referencias a **system_function_schema** con **dbo** en todos los scripts que contengan instrucciones DDL de funciones definidas por el usuario.  
  
5.  Modificar los scripts que invocan estas funciones para usar el nombre de dos partes dbo **.** _function_name_, o el nombre de tres partes _database_name_**.** dbo. *nombre_función*.  
  
 Para obtener más información, vea los temas siguientes en los Libros en pantalla de SQL Server:  
  
-   "sp_changeobjectowner"  
  
-   "Separación de esquemas de usuario"  
  
-   "Base de datos Resource"  
  
## <a name="see-also"></a>Vea también  
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)   
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Quite las instrucciones que modifican objetos del sistema](../../../2014/sql-server/install/remove-statements-that-modify-system-objects.md)   
 [Quitar instrucciones que quiten objetos del sistema](../../../2014/sql-server/install/remove-statements-that-drop-system-objects.md)  
  
  

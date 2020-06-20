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
ms.openlocfilehash: 7242f9fda74288a2b7354ac0550ff4966e05c555
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058783"
---
# <a name="user-defined-functions-are-not-allowed-in-system_function_schema"></a>Las funciones definidas por el usuario no se permiten en system_function_schema
  El asesor de actualizaciones detectó funciones definidas por el usuario que son propiedad del usuario no documentado **system_function_schema**. No puede crear una función del sistema definida por el usuario especificando este usuario. El nombre de usuario **system_function_schema** no existe y el ID. de usuario asociado a este nombre (UID = 4) está reservado para el esquema **Sys** y está restringido exclusivamente al uso interno.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 El almacenamiento de objetos del sistema y el acceso han cambiado de las siguientes maneras:  
  
-   Los objetos del sistema se almacenan en la base de datos de **recursos** de solo lectura y no se permiten las actualizaciones directas de objetos del sistema.  
  
     Los objetos del sistema aparecen lógicamente en el esquema **Sys** de todas las bases de datos. Esto mantiene la capacidad de invocar funciones del sistema desde cualquier base de datos especificando un nombre de función con una sola parte. Por ejemplo, la instrucción `SELECT * FROM fn_helpcollations()` se puede ejecutar desde cualquier base de datos.  
  
-   Se ha quitado el **system_function_schema** de usuario no documentado.  
  
-   El ID. de usuario asociado a **system_function_schema** (UID = 4) se reserva para el esquema **Sys** y está restringido exclusivamente al uso interno.  
  
 Estos cambios tienen el efecto siguiente sobre las funciones del sistema definidas por el usuario:  
  
-   Se producirá un error en las instrucciones del lenguaje de definición de datos (DDL) que hacen referencia a **system_function_schema** . Por ejemplo, la instrucción `CREATE FUNCTION system` _ `function` \_ `schema.fn` \_ `MySystemFunction` ... no se realizará correctamente.  
  
-   Después de actualizar a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] , los objetos existentes que son propiedad de **system_function_schema** solo se incluyen en el esquema **Sys** de la base de datos **maestra** . Dado que no se pueden modificar los objetos del sistema, estas funciones nunca se pueden cambiar o quitar de la base de datos **maestra** . Además, estas funciones no se pueden invocar desde otras bases de datos especificando solo un nombre de función con una parte.  
  
## <a name="corrective-action"></a>Acción correctora  
 Antes de actualizar, lleve a cabo las siguientes tareas:  
  
1.  Cambiar la propiedad de las funciones definidas por el usuario existentes a **DBO** mediante el **sp_changeobjectowner** procedimiento almacenado del sistema.  
  
2.  Considere cambiar el nombre de la función para que no utilice el prefijo 'fn_'. Esto evitará conflictos potenciales del nombre con otras funciones del sistema existentes o futuras.  
  
3.  Agregue una copia de las funciones modificadas en cada base de datos que las utilice.  
  
4.  Reemplace las referencias a **system_function_schema** con **DBO** en todos los scripts que CONtengan instrucciones DDL de funciones definidas por el usuario.  
  
5.  Modifique los scripts que invocan estas funciones para usar el nombre DBO de dos partes **.** _function_name_o el nombre de tres partes _database_name_**.** DBO. *function_name*.  
  
 Para obtener más información, vea los temas siguientes en los Libros en pantalla de SQL Server:  
  
-   "sp_changeobjectowner"  
  
-   "Separación de esquemas de usuario"  
  
-   "Base de datos Resource"  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)   
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Quitar instrucciones que modifican objetos del sistema](../../../2014/sql-server/install/remove-statements-that-modify-system-objects.md)   
 [Quitar instrucciones que quiten objetos del sistema](../../../2014/sql-server/install/remove-statements-that-drop-system-objects.md)  
  
  

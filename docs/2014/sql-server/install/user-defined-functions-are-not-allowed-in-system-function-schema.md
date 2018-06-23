---
title: Funciones definidas por el usuario no se permiten en system_function_schema | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- system functions [SQL Server]
- user-defined functions [SQL Server], system
ms.assetid: 3cb54053-ef65-4558-ae96-8686b6b22f4f
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 16c6cf618028d56a3b09cdad8da4cfd9eb9309f4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111270"
---
# <a name="user-defined-functions-are-not-allowed-in-systemfunctionschema"></a>Las funciones definidas por el usuario no se permiten en system_function_schema
  El Asesor de actualizaciones detectó funciones definidas por el usuario que son propiedad del usuario no documentado **system_function_schema**. No puede crear una función del sistema definida por el usuario especificando este usuario. El **system_function_schema** nombre de usuario no existe, y el identificador de usuario que está asociado con este nombre (UID = 4) se reserva para el **sys** esquema y se restringe a solo para uso interno.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 El almacenamiento de objetos del sistema y el acceso han cambiado de las siguientes maneras:  
  
-   Objetos del sistema se almacenan en solo lectura **recursos** base de datos y dirigir actualizaciones del objeto de sistema no están permitidas.  
  
     Objetos del sistema aparecen lógicamente en el **sys** esquema de cada base de datos. Esto mantiene la capacidad de invocar funciones del sistema desde cualquier base de datos especificando un nombre de función con una sola parte. Por ejemplo, la instrucción `SELECT * FROM fn_helpcollations()` se puede ejecutar desde cualquier base de datos.  
  
-   El usuario no documentado **system_function_schema** se ha quitado.  
  
-   El usuario ID asociado con **system_function_schema** (UID = 4) se reserva para el **sys** esquema y se restringe a solo para uso interno.  
  
 Estos cambios tienen el efecto siguiente sobre las funciones del sistema definidas por el usuario:  
  
-   Instrucciones de lenguaje de definición (DDL) de datos que hacen referencia a **system_function_schema** se producirá un error. Por ejemplo, la instrucción `CREATE FUNCTION system`_`function` \_ `schema.fn` \_ `MySystemFunction` ... no tendrán éxito.  
  
-   Después de actualizar a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], los objetos existentes que pertenecen a **system_function_schema** solo están contenidos en el **sys** esquema de la **maestro** base de datos. Dado que no se puede modificar los objetos del sistema, estas funciones nunca se pueden modificar o quitar de la **maestro** base de datos. Además, estas funciones no se pueden invocar desde otras bases de datos especificando solo un nombre de función con una parte.  
  
## <a name="corrective-action"></a>Acción correctora  
 Antes de actualizar, lleve a cabo las siguientes tareas:  
  
1.  Cambiar la propiedad de las funciones definidas por el usuario existentes a **dbo** mediante el uso de la **sp_changeobjectowner** procedimiento almacenado del sistema.  
  
2.  Considere cambiar el nombre de la función para que no utilice el prefijo 'fn_'. Esto evitará conflictos potenciales del nombre con otras funciones del sistema existentes o futuras.  
  
3.  Agregue una copia de las funciones modificadas en cada base de datos que las utilice.  
  
4.  Reemplace las referencias a **system_function_schema** con **dbo** en todos los scripts que contienen instrucciones de DDL de funciones definidas por el usuario.  
  
5.  Modifique los scripts que invocan estas funciones para utilizar ya sea el nombre de dos partes dbo **. *** nombre_función*, o el nombre de tres partes *database_name ***.** dbo.* nombre_función *.  
  
 Para obtener más información, vea los temas siguientes en los Libros en pantalla de SQL Server:  
  
-   "sp_changeobjectowner"  
  
-   "Separación de esquemas de usuario"  
  
-   "Base de datos Resource"  
  
## <a name="see-also"></a>Vea también  
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)   
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Quite las instrucciones que modifican objetos del sistema](../../../2014/sql-server/install/remove-statements-that-modify-system-objects.md)   
 [Quitar instrucciones que quiten objetos del sistema](../../../2014/sql-server/install/remove-statements-that-drop-system-objects.md)  
  
  

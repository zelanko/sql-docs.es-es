---
title: MSSQLSERVER_208 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 208 (Database Engine error)
ms.assetid: 4b1895f5-3197-4da1-af86-954c93507956
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 97ab3eb220c03c3de0c95251861f3b947890b090
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85034662"
---
# <a name="mssqlserver_208"></a>MSSQLSERVER_208
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|208|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQ_BADOBJECT|  
|Texto del mensaje|El nombre de objeto '%.*ls' no es válido.|  
  
## <a name="explanation"></a>Explicación  
 No se encuentra el objeto especificado.  
  
### <a name="possible-causes"></a>Causas posibles  
 Este error puede deberse a uno de los siguientes problemas:  
  
-   No se ha especificado correctamente el objeto.  
  
-   El objeto no existe en la base de datos actual o en la base de datos especificada.  
  
-   El objeto existe, pero no ha podido mostrarse al usuario. Por ejemplo, puede que el usuario no tenga permisos para el objeto o que el objeto se haya creado dentro de una instrucción EXECUTE pero se tenga acceso a él fuera del ámbito de la citada instrucción.  
  
## <a name="user-action"></a>Acción del usuario  
 Compruebe la información siguiente y corrija la instrucción según corresponda.  
  
-   El nombre de objeto está escrito correctamente.  
  
-   El contexto de base de datos actual es correcto. Si no se especifica un nombre de base de datos para el objeto, este debe existir en la base de datos actual. Para obtener más información sobre cómo establecer el contexto de base de datos, vea [USE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql).  
  
-   El objeto existe en las tablas del sistema. Para comprobar si existe una tabla u otro objeto del ámbito de esquema, vea la vista de catálogo **sys.objects**. Si el objeto no está en las tablas del sistema, significa que se ha eliminado o que el usuario no tiene permisos para ver los metadatos del objeto. Para obtener más información sobre los permisos de visualización de los metadatos de objeto, vea [Configuración de visibilidad de los metadatos](../security/metadata-visibility-configuration.md).  
  
-   El objeto está contenido en el esquema predeterminado del usuario. De lo contrario, el objeto se debe especificar usando el formato de dos partes *schema_name.object_name*. Observe que las funciones escalares siempre deben invocarse utilizando como mínimo un nombre de dos partes.  
  
-   La distinción entre mayúsculas y minúsculas de la intercalación de bases de datos.  
  
     Cuando una base de datos utiliza una intercalación con distinción entre mayúsculas y minúsculas, las mayúsculas y minúsculas del nombre de objeto deben coincidir con las del objeto en la base de datos. Por ejemplo, cuando un objeto se especifica como **MyTable** en una base de datos con una intercalación con distinción entre mayúsculas y minúsculas, las consultas que hagan referencia al objeto como **mytable** o **Mytable** harán que se devuelva el error 208 porque los nombres de objeto no coinciden.  
  
     Puede comprobar la intercalación de bases de datos ejecutando la instrucción siguiente.  
  
    ```  
    SELECT collation_name FROM sys.databases WHERE name = 'database_name';  
    ```  
  
     La abreviatura CS en el nombre de la intercalación indica que esta distingue entre mayúsculas y minúsculas. Por ejemplo, Latin1_General_CS_AS es una intercalación con distinción entre mayúsculas y minúsculas, y con distinción de acentos. CI indica una intercalación sin distinción entre mayúsculas y minúsculas.  
  
-   El usuario dispone de permiso para tener acceso al objeto. Para comprobar los permisos que tiene el usuario para el objeto, use la función del sistema **Has_Perms_By_Name**.  
  
## <a name="see-also"></a>Consulte también  
 [USAR &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql)   
 [Configuración de visibilidad de los metadatos](../security/metadata-visibility-configuration.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/has-perms-by-name-transact-sql)  
  
  

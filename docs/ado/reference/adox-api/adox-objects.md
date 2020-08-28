---
description: Objetos ADOX
title: Objetos ADOX | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- objects [ADOX]
- ADOX, objects
ms.assetid: 3f5287e9-f62c-40c4-bb59-985102be956e
author: rothja
ms.author: jroth
ms.openlocfilehash: c38b184164109ee3e6fed18a439cd904119a3ec6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985666"
---
# <a name="adox-objects"></a>Objetos ADOX
## <a name="adox-object-summary"></a>Resumen de objetos ADOX  
  
|Object|Descripción|  
|------------|-----------------|  
|[Catálogo](./catalog-object-adox.md)|Contiene colecciones que describen el catálogo de esquema de un origen de datos.|  
|[Columna](./column-object-adox.md)|Representa una columna de una tabla, un índice o una clave.|  
|[Grupo](./group-object-adox.md)|Representa una cuenta de grupo que tiene permisos de acceso en una base de datos protegida.|  
|[Index](./index-object-adox.md)|Representa un índice de una tabla de base de datos.|  
|[Clave](./key-object-adox.md)|Representa un campo de clave principal, externa o única de una tabla de base de datos.|  
|[Procedimiento](./procedure-object-adox.md)|Representa un procedimiento almacenado.|  
|[Table](./table-object-adox.md)|Representa una tabla de base de datos, que incluye columnas, índices y claves.|  
|[Usuario](./user-object-adox.md)|Representa una cuenta de usuario que tiene permisos de acceso en una base de datos protegida.|  
|[Ver](./view-object-adox.md)|Representa un conjunto filtrado de registros o una tabla virtual.|  
  
 Las relaciones entre estos objetos se ilustran en el [modelo de objetos ADOX](./adox-object-model.md).  
  
 Cada objeto puede estar contenido en su colección correspondiente. Por ejemplo, un objeto **TABLE** puede estar contenido en una colección [tables](./tables-collection-adox.md) . Para obtener más información, vea [colecciones de ADOX](./adox-collections.md) o un tema específico de la colección.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API de ADOX](./adox-object-model.md?view=sql-server-ver15)   
 [Colecciones de ADOX](./adox-collections.md)   
 [Modelo de objetos ADOX](./adox-object-model.md)   
 [Extensiones de ADO para lenguaje de definición de datos y seguridad (ADOX)](../../guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)
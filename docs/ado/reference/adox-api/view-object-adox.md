---
title: Ver el objeto (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- View
helpviewer_keywords:
- View object [ADOX]
ms.assetid: 653421ce-7b94-43d0-9bc6-4900f8f2af45
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d87b56716ed1876acc6ac139e7804036d5cdfb86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718811"
---
# <a name="view-object-adox"></a>Objeto View (ADOX)
Representa un conjunto filtrado de registros o una tabla virtual. Cuando se usa junto con la propiedad ADO [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto, el **vista** objeto puede utilizarse para agregar, eliminar o modificar vistas.  
  
## <a name="remarks"></a>Comentarios  
 Una vista es una tabla virtual, creada a partir de otras tablas de base de datos o vistas. El **vista** objeto le permite crear una vista sin necesidad de conocer ni utilizar la sintaxis del proveedor "CREATE VIEW".  
  
 Con las propiedades de un **vista** de objeto, puede:  
  
-   Identificar la vista con el [nombre](../../../ado/reference/adox-api/name-property-adox.md) propiedad.  
  
-   Especifique la propiedad ADO **comando** objeto que puede usarse para agregar, eliminar o modificar vistas con la [comando](../../../ado/reference/adox-api/command-property-adox.md) propiedad.  
  
-   Devolver información de fecha con el [DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md) y [DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md) propiedades.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto View](../../../ado/reference/adox-api/view-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Las vistas y ejemplo de colecciones de campos (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Vistas de ejemplo de método Append (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Colección de vistas, ejemplo de la propiedad CommandText (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Eliminación de vistas de ejemplo del método (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Colección de vistas (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)

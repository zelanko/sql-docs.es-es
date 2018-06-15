---
title: Clave (objeto) (ADOX) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Key
helpviewer_keywords:
- Key object [ADOX]
ms.assetid: 55f116fe-4d56-4892-bffe-0cdd6fc727c9
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 05863d8227f2f0dddc6b7a44c60951fe3f8471be
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35286844"
---
# <a name="key-object-adox"></a>Objeto Key (ADOX)
Representa un campo de clave principal, externo o único de una tabla de base de datos.  
  
## <a name="remarks"></a>Notas  
 El siguiente código crea un nuevo **clave**:  
  
```  
Dim obj As New Key  
```  
  
 Con las propiedades y colecciones de una **clave** de objeto, puede:  
  
-   Identificar la clave con el [nombre](../../../ado/reference/adox-api/name-property-adox.md) propiedad.  
  
-   Determinar si la clave es principal, externa o única con la [tipo](../../../ado/reference/adox-api/type-property-key-adox.md) propiedad.  
  
-   Acceso a las columnas de base de datos de la clave con el [columnas](../../../ado/reference/adox-api/columns-collection-adox.md) colección.  
  
-   Especifique el nombre de la tabla relacionada con la [RelatedTable](../../../ado/reference/adox-api/relatedtable-property-adox.md) propiedad.  
  
-   Determinar la acción realizada al eliminar o actualizar una clave principal con el [DeleteRule](../../../ado/reference/adox-api/deleterule-property-adox.md) y [UpdateRule](../../../ado/reference/adox-api/updaterule-property-adox.md) propiedades.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto Key](../../../ado/reference/adox-api/key-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Anexar de teclas de método, tipo de clave, RelatedColumn, RelatedTable y ejemplo de las propiedades UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Colección de columnas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Colección de claves (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)

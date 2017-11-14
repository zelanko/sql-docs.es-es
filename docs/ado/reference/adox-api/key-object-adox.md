---
title: Clave (objeto) (ADOX) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Key
helpviewer_keywords:
- Key object [ADOX]
ms.assetid: 55f116fe-4d56-4892-bffe-0cdd6fc727c9
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7d05a52614694bc9464c609ab4f4ed0965f3b81e
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="key-object-adox"></a>Objeto Key (ADOX)
Representa un campo de clave principal, externo o único de una tabla de base de datos.  
  
## <a name="remarks"></a>Comentarios  
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
  
-   [Eventos, métodos y propiedades del objeto de clave](../../../ado/reference/adox-api/key-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Anexar de teclas de método, tipo de clave, RelatedColumn, RelatedTable y ejemplo de las propiedades UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Colección de columnas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Colección de claves (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)


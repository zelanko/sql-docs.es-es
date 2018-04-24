---
title: Precision (propiedad, ADOX) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::put_Precision
- _Column::PutPrecision
- _Column::GetPrecision
- _Column::get_Precision
- _Column::Precision
helpviewer_keywords:
- Precision property [ADOX]
ms.assetid: 0e0ecbbf-d7de-49d4-a128-5a519ecd54ba
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 790f4dafda40218e40c9fd88826838814177e72b
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="precision-property-adox"></a>Precision (propiedad, ADOX)
Indica la precisión máxima de valores de datos de la [columna](../../../ado/reference/adox-api/column-object-adox.md).  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece y devuelve un **largo** valor que es la precisión máxima de valores de datos de la columna cuando la [tipo](../../../ado/reference/adox-api/type-property-column-adox.md) propiedad es un tipo numérico. **Precisión** se omite para todos los demás tipos de datos.  
  
## <a name="remarks"></a>Comentarios  
 El valor predeterminado es cero (**0**).  
  
 Esta propiedad es de solo lectura para [columna](../../../ado/reference/adox-api/column-object-adox.md) ya anexados a una colección de objetos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de código ADOX: NumericScale y ejemplo de las propiedades Precision (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Tipo de propiedad (columna) (ADOX)](../../../ado/reference/adox-api/type-property-column-adox.md)   
 [Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)

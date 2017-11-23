---
title: NumericScale (propiedad, ADOX) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Column::PutNumericScale
- _Column::GetNumericScale
- _Column::NumericScale
- _Column::put_NumericScale
- _Column::get_NumericScale
helpviewer_keywords: NumericScale property [ADOX]
ms.assetid: 573ee5d1-57c7-4a27-be79-a0e12944ad9b
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 719c0164cd33f3d88f07c77414f7105e17b2477d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="numericscale-property-adox"></a>NumericScale (propiedad, ADOX)
Indica la escala de un valor numérico en la columna.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece y devuelve un **bytes** valor que es la escala de valores de datos de la columna cuando la [tipo](../../../ado/reference/adox-api/type-property-column-adox.md) propiedad es **adNumeric** o **adDecimal**. **NumericScale** se omite para todos los demás tipos de datos.  
  
## <a name="remarks"></a>Comentarios  
 El valor predeterminado es cero (0).  
  
 **NumericScale** es de solo lectura para [columna](../../../ado/reference/adox-api/column-object-adox.md) ya anexados a una colección de objetos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de código ADOX: NumericScale y ejemplo de las propiedades Precision (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Type (propiedad, columna, ADOX)](../../../ado/reference/adox-api/type-property-column-adox.md)

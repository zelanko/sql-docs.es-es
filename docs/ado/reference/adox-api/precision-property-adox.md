---
description: Precision (propiedad, ADOX)
title: Propiedad Precision (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0e75cfa88eb66b88084a823d0558923210aed4db
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769785"
---
# <a name="precision-property-adox"></a>Precision (propiedad, ADOX)
Indica la precisión máxima de los valores de datos de la [columna](./column-object-adox.md).  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece y devuelve un valor **Long** que es la precisión máxima de los valores de datos de la columna cuando la propiedad [Type](./type-property-column-adox.md) es un tipo numérico. La **precisión** se omite para todos los demás tipos de datos.  
  
## <a name="remarks"></a>Observaciones  
 El valor predeterminado es cero (**0**).  
  
 Esta propiedad es de solo lectura para los objetos de [columna](./column-object-adox.md) ya anexados a una colección.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Column (ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de código ADOX: ejemplo de propiedades NumericScale y Precision (VB)](./adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Type (propiedad, Column) (ADOX)](./type-property-column-adox.md)   
 [Objeto Column (ADOX)](./column-object-adox.md)
---
description: Type (propiedad, columna, ADOX)
title: Propiedad Type (Column) (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::Type
- _Column::GetType
- _Column::get_Type
- _Column::put_Type
- _Column::PutType
helpviewer_keywords:
- Type property [ADOX]
ms.assetid: 5c6718b6-f728-478a-8afb-5d17b0a91d1f
author: rothja
ms.author: jroth
ms.openlocfilehash: 70d8700f953a87fa3326f6a1c0985be1f6ca3dac
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769224"
---
# <a name="type-property-column-adox"></a>Type (propiedad, columna, ADOX)
Indica el tipo de datos de una columna.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor **Long** que puede ser una de las constantes [DataTypeEnum](../ado-api/datatypeenum.md) . El valor predeterminado es **adVarWChar**.  
  
## <a name="remarks"></a>Observaciones  
 Esta propiedad es de lectura/escritura hasta que el objeto de [columna](./column-object-adox.md) se anexa a una colección o a otro objeto, después del cual es de solo lectura.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Column (ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedad ParentCatalog (VB)](./parentcatalog-property-example-vb.md)   
 [Type (propiedad, Key) (ADOX)](./type-property-key-adox.md)   
 [Type (propiedad, tabla, ADOX)](./type-property-table-adox.md)
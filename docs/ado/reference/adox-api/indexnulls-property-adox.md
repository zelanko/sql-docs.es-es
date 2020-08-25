---
description: IndexNulls (propiedad, ADOX)
title: IndexNulls (propiedad, ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Index::get_IndexNulls
- _Index::GetIndexNulls
- _Index::put_IndexNulls
- _Index::PutIndexNulls
- _Index::IndexNulls
helpviewer_keywords:
- IndexNulls property [ADOX]
ms.assetid: 313b0bf7-3f37-4823-8fca-bd9c80e078a7
author: rothja
ms.author: jroth
ms.openlocfilehash: 7b71e3298c18b10fa34615e3382d561f454b5eb4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770174"
---
# <a name="indexnulls-property-adox"></a>IndexNulls (propiedad, ADOX)
Indica si los registros que tienen valores NULL en sus campos de índice tienen entradas de índice.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece y devuelve un valor de [AllowNullsEnum](./allownullsenum.md) . El valor predeterminado es **adIndexNullsDisallow**.  
  
## <a name="remarks"></a>Observaciones  
 Esta propiedad es de solo lectura en los objetos de [Índice](./index-object-adox.md) ya anexados a una colección.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Index (ADOX)](./index-object-adox.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedad IndexNulls (VB)](./indexnulls-property-example-vb.md)
---
description: Attributes (propiedad, ADOX)
title: Attributes (propiedad, ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::put_Attributes
- _Column::Attributes
- _Column::PutAttributes
- _Column::get_Attributes
- _Column::GetAttributes
helpviewer_keywords:
- Attributes property [ADOX]
ms.assetid: e3abb359-79a3-4c22-b3a8-2900817e0d23
author: rothja
ms.author: jroth
ms.openlocfilehash: b2fca7e2cf9bce25d1993d16d4ec6a44bf53ef67
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771354"
---
# <a name="attributes-property-adox"></a>Attributes (propiedad, ADOX)
Describe las características de las columnas.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor **Long** . El valor especifica las características de la tabla representada por el objeto de [columna](./column-object-adox.md) . El valor puede ser una combinación de constantes [ColumnAttributesEnum](./columnattributesenum.md) . El valor predeterminado es cero (**0**), que no es ni **adColFixed** ni **adColNullable**.  
  
## <a name="applies-to"></a>Se aplica a  
  
- [Objeto Column (ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedad Attributes (VB)](./attributes-property-example-vb.md)
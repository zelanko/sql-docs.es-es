---
title: AllowNullsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AllowNullsEnum
helpviewer_keywords:
- AllowNullsEnum enumeration [ADOX]
ms.assetid: 6acf3689-1a7f-4379-9d7f-df452ccbac27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9d1f4f5ce302c6f9e3e28b037c838d452f771114
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692693"
---
# <a name="allownullsenum"></a>AllowNullsEnum
Especifica si se indizan los registros con valores null.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|El índice permite entradas en el que las columnas de clave son nulos. Si se escribe un valor null en una columna de clave, la entrada se inserta en el índice.|  
|**adIndexNullsDisallow**|1|Predeterminado: El índice no permite entradas en el que las columnas de clave son nulos. Si se especifica un valor null en una columna de clave, se producirá un error.|  
|**adIndexNullsIgnore**|2|El índice no inserta las entradas que contienen las claves null. Si se especifica un valor null en una columna de clave, se omite la entrada y se produce ningún error.|  
|**adIndexNullsIgnoreAny**|4|El índice no inserta entradas que alguna columna de clave tiene un valor null. Para un índice que tenga una columna en varias claves, si se especifica un valor nulo en alguna columna, se omite la entrada y se produce ningún error.|  
  
## <a name="applies-to"></a>Se aplica a  
 [IndexNulls (propiedad, ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)

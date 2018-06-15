---
title: AllowNullsEnum | Documentos de Microsoft
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
- AllowNullsEnum
helpviewer_keywords:
- AllowNullsEnum enumeration [ADOX]
ms.assetid: 6acf3689-1a7f-4379-9d7f-df452ccbac27
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 49d0ef3d6de71281d403fafe71bf0df835c8985d
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35284844"
---
# <a name="allownullsenum"></a>AllowNullsEnum
Especifica si se indizan registros con valores null.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|El índice permite entradas en el que las columnas de clave son nulos. Si se especifica un valor null en una columna de clave, la entrada se inserta en el índice.|  
|**adIndexNullsDisallow**|1|Predeterminado: El índice no permite entradas en las que las columnas de clave son null. Si se especifica un valor null en una columna de clave, se producirá un error.|  
|**adIndexNullsIgnore**|2|El índice no inserta entradas que contengan claves nulas. Si se especifica un valor null en una columna de clave, la entrada se omite y se produce ningún error.|  
|**adIndexNullsIgnoreAny**|4|El índice no inserta entradas en alguna columna clave tiene un valor null. Para un índice que tenga una columna de la clave, si se especifica un valor nulo en alguna columna, se omite la entrada y se produce ningún error.|  
  
## <a name="applies-to"></a>Se aplica a  
 [IndexNulls (propiedad, ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)

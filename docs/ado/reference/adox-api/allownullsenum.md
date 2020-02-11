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
ms.openlocfilehash: 48e9d8c40d2ab76b902d285526fcd9e9abf7be07
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67967331"
---
# <a name="allownullsenum"></a>AllowNullsEnum
Especifica si los registros con valores NULL se indizan.  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|El índice permite entradas en las que las columnas de clave sean null. Si se especifica un valor null en una columna de clave, la entrada se inserta en el índice.|  
|**adIndexNullsDisallow**|1|Default. El índice no permite entradas en las que las columnas de clave sean null. Si se especifica un valor null en una columna de clave, se producirá un error.|  
|**adIndexNullsIgnore**|2|El índice no inserta entradas que contengan claves nulas. Si se especifica un valor null en una columna de clave, la entrada se omite y no se produce ningún error.|  
|**adIndexNullsIgnoreAny**|4|El índice no inserta entradas en las que alguna columna de clave tenga un valor null. En el caso de un índice que tenga una clave de varias columnas, si se especifica un valor null en alguna columna, se omitirá la entrada y no se producirá ningún error.|  
  
## <a name="applies-to"></a>Se aplica a  
 [IndexNulls (propiedad, ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)

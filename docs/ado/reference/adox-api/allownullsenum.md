---
description: AllowNullsEnum
title: AllowNullsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c2d21b4a7e4de67e45210f11598a7cf3a2a99b9e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985546"
---
# <a name="allownullsenum"></a>AllowNullsEnum
Especifica si los registros con valores NULL se indizan.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|El índice permite entradas en las que las columnas de clave sean null. Si se especifica un valor null en una columna de clave, la entrada se inserta en el índice.|  
|**adIndexNullsDisallow**|1|Predeterminada. El índice no permite entradas en las que las columnas de clave sean null. Si se especifica un valor null en una columna de clave, se producirá un error.|  
|**adIndexNullsIgnore**|2|El índice no inserta entradas que contengan claves nulas. Si se especifica un valor null en una columna de clave, la entrada se omite y no se produce ningún error.|  
|**adIndexNullsIgnoreAny**|4|El índice no inserta entradas en las que alguna columna de clave tenga un valor null. En el caso de un índice que tenga una clave de varias columnas, si se especifica un valor null en alguna columna, se omitirá la entrada y no se producirá ningún error.|  
  
## <a name="applies-to"></a>Se aplica a  
 [IndexNulls (propiedad, ADOX)](./indexnulls-property-adox.md)
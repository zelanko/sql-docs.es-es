---
title: PositionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PositionEnum
helpviewer_keywords:
- PositionEnum enumeration
ms.assetid: e69af0a5-3405-4b72-9c6e-6b188ff746fd
author: rothja
ms.author: jroth
ms.openlocfilehash: 6a61dae9888628302da3326a1465f4182c49e39c
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243226"
---
# <a name="positionenum"></a>PositionEnum
Especifica la posición actual del puntero de registro dentro de un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|Indica que el puntero del registro actual está en BOF (es decir, la propiedad [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) es **true**).|  
|**adPosEOF**|-3|Indica que el puntero del registro actual está en EOF (es decir, la propiedad [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) es **true**).|  
|**adPosUnknown**|-1|Indica que el **conjunto de registros** está vacío, se desconoce la posición actual o el proveedor no admite la propiedad [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) o [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) .|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. position. BOF|  
|AdoEnums. position. EOF|  
|AdoEnums. position. UNKNOWN|  
  
## <a name="applies-to"></a>Se aplica a  

:::row:::
    :::column:::
        [Propiedad AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)  
    :::column-end:::
    :::column:::
        [Propiedad AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)  
    :::column-end:::
:::row-end:::

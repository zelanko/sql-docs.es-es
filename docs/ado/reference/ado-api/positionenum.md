---
description: PositionEnum
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
ms.openlocfilehash: 326fc4f1b9b77c8a4470fedc7d55f2d379aff6f3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442717"
---
# <a name="positionenum"></a>PositionEnum
Especifica la posición actual del puntero de registro dentro de un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Value|Descripción|  
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

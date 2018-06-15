---
title: PositionEnum | Documentos de Microsoft
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
- PositionEnum
helpviewer_keywords:
- PositionEnum enumeration
ms.assetid: e69af0a5-3405-4b72-9c6e-6b188ff746fd
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d32d2e507b8ca7214eb142160c65f953771f4527
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35280753"
---
# <a name="positionenum"></a>PositionEnum
Especifica la posición actual del puntero de registro dentro de un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|Indica que el puntero del registro actual está en BOF (es decir, el [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) propiedad es **True**).|  
|**adPosEOF**|-3|Indica que el puntero del registro actual está en EOF (es decir, el [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) propiedad es **True**).|  
|**adPosUnknown**|-1|Indica que la **Recordset** está vacío, se desconoce la posición actual o el proveedor no admite la [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) o [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) propiedad.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.Position.BOF|  
|AdoEnums.Position.EOF|  
|AdoEnums.Position.UNKNOWN|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Propiedad AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)|[Propiedad AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|

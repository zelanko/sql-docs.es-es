---
title: CursorTypeEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: CursorTypeEnum
helpviewer_keywords: CursorTypeEnum enumeration [ADO]
ms.assetid: ffc6e245-4471-42ae-84dd-e85bddfce983
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5adf070387078902d7d21a68cc0f89af2de8194a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="cursortypeenum"></a>CursorTypeEnum
Especifica el tipo de cursor que se utiliza en una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adOpenDynamic**|2|Utiliza un cursor dinámico. Las adiciones, cambios y eliminaciones realizadas por otros usuarios son visibles y todos los tipos de movimiento a través de la **Recordset** tienen, excepto para marcadores, si el proveedor no los admite.|  
|**adOpenForwardOnly**|0|Predeterminado: Utiliza un cursor de solo avance. Es idéntico a un cursor estático, excepto que solo puede desplazarse hacia delante por los registros. Esto mejora el rendimiento cuando deba realizar solo uno pasar a través de un **conjunto de registros**.|  
|**adOpenKeyset**|1|Utiliza un cursor de conjunto de claves. Al igual que un cursor dinámico, salvo que no puede ver los registros que se agregan otros usuarios, aunque los registros que se eliminan mediante otros usuarios son inaccesibles desde su **conjunto de registros**. Cambios en los datos por otros usuarios siguen siendo visibles.|  
|**adOpenStatic**|3|Utiliza un cursor estático, que es una copia estática de un conjunto de registros que puede usar para buscar datos o generar informes. Las adiciones, cambios o eliminaciones realizadas por otros usuarios no son visibles.|  
|**adOpenUnspecified**|-1|No especifica el tipo de cursor.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.CursorType.DYNAMIC|  
|AdoEnums.CursorType.FORWARDONLY|  
|AdoEnums.CursorType.KEYSET|  
|AdoEnums.CursorType.STATIC|  
|AdoEnums.CursorType.UNSPECIFIED|  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad CursorType (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)

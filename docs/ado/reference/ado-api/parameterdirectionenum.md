---
title: ParameterDirectionEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ParameterDirectionEnum
helpviewer_keywords: ParameterDirectionEnum enumeration [ADO]
ms.assetid: c66aa6e6-d4f0-4f0f-9640-e08ae6cfdef3
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 51083883a293bb44c76cadf3971e920e8c3ed05c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="parameterdirectionenum"></a>ParameterDirectionEnum
Especifica si el [parámetro](../../../ado/reference/ado-api/parameter-object.md) representa un parámetro de entrada, un parámetro de salida, tanto de entrada y un parámetro de salida o el valor devuelto de un procedimiento almacenado.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adParamInput**|1|Predeterminado: Indica que el parámetro representa un parámetro de entrada.|  
|**adParamInputOutput**|3|Indica que el parámetro representa un parámetro de entrada y salido.|  
|**adParamOutput**|2|Indica que el parámetro representa un parámetro de salida.|  
|**adParamReturnValue**|4|Indica que el parámetro representa un valor devuelto.|  
|**adParamUnknown**|0|Indica que la dirección del parámetro es desconocida.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.ParameterDirection.INPUT|  
|AdoEnums.ParameterDirection.INPUTOUTPUT|  
|AdoEnums.ParameterDirection.OUTPUT|  
|AdoEnums.ParameterDirection.RETURNVALUE|  
|AdoEnums.ParameterDirection.UNKNOWN|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)|[Propiedad Direction](../../../ado/reference/ado-api/direction-property.md)|

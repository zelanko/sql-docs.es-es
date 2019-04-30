---
title: ParameterDirectionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ParameterDirectionEnum
helpviewer_keywords:
- ParameterDirectionEnum enumeration [ADO]
ms.assetid: c66aa6e6-d4f0-4f0f-9640-e08ae6cfdef3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01f423652f32b9afe801ef99e299f65a6a860a8a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63314832"
---
# <a name="parameterdirectionenum"></a>ParameterDirectionEnum
Especifica si el [parámetro](../../../ado/reference/ado-api/parameter-object.md) representa un parámetro de entrada, un parámetro de salida, una entrada y un parámetro de salida o el valor devuelto de un procedimiento almacenado.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adParamInput**|1|Predeterminado: Indica que el parámetro representa un parámetro de entrada.|  
|**adParamInputOutput**|3|Indica que el parámetro representa un parámetro de entrada y salido.|  
|**adParamOutput**|2|Indica que el parámetro representa un parámetro de salida.|  
|**adParamReturnValue**|4|Indica que el parámetro representa un valor devuelto.|  
|**adParamUnknown**|0|Indica que la dirección del parámetro es desconocida.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Package: **com.ms.wfc.data**  
  
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

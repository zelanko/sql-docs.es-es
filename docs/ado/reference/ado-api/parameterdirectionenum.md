---
description: ParameterDirectionEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: cdd0e393c7fc5214866142150c7ff497e48e7122
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773334"
---
# <a name="parameterdirectionenum"></a>ParameterDirectionEnum
Especifica si el [parámetro](./parameter-object.md) representa un parámetro de entrada, un parámetro de salida, una entrada y un parámetro de salida, o el valor devuelto de un procedimiento almacenado.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adParamInput**|1|Predeterminada. Indica que el parámetro representa un parámetro de entrada.|  
|**adParamInputOutput**|3|Indica que el parámetro representa un parámetro de entrada y de salida.|  
|**adParamOutput**|2|Indica que el parámetro representa un parámetro de salida.|  
|**adParamReturnValue**|4|Indica que el parámetro representa un valor devuelto.|  
|**adParamUnknown**|0|Indica que la dirección del parámetro es desconocida.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. ParameterDirection. INPUT|  
|AdoEnums. ParameterDirection. INPUTOUTPUT|  
|AdoEnums. ParameterDirection. OUTPUT|  
|AdoEnums. ParameterDirection. RETURNVALUE|  
|AdoEnums. ParameterDirection. UNKNOWN|  
  
## <a name="applies-to"></a>Se aplica a  

:::row:::
    :::column:::
        [Método CreateParameter (ADO)](./createparameter-method-ado.md)  
    :::column-end:::
    :::column:::
        [Propiedad Direction](./direction-property.md)  
    :::column-end:::
:::row-end:::
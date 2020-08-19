---
description: ObjectStateEnum
title: ObjectStateEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ObjectStateEnum
helpviewer_keywords:
- ObjectStateEnum enumeration [ADO]
ms.assetid: 32746558-097b-4749-989e-519aadf7e3f4
author: rothja
ms.author: jroth
ms.openlocfilehash: 0c387240e36225f03c8ba1287618ab59a98fb63c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443027"
---
# <a name="objectstateenum"></a>ObjectStateEnum
Especifica si un objeto está abierto o cerrado, se está conectando a un origen de datos, ejecutando un comando o recuperando datos.  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|Indica que el objeto está cerrado.|  
|**adStateOpen**|1|Indica que el objeto está abierto.|  
|**adStateConnecting**|2|Indica que el objeto se está conectando.|  
|**adStateExecuting**|4|Indica que el objeto está ejecutando un comando.|  
|**adStateFetching**|8|Indica que se están recuperando las filas del objeto.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. ObjectState. CLOSED|  
|AdoEnums. ObjectState. OPEN|  
|AdoEnums. ObjectState. CONNECTing|  
|AdoEnums.ObjectState.EXECUTING|  
|AdoEnums. ObjectState. FETCH|  
  
## <a name="applies-to"></a>Se aplica a  

:::row:::
    :::column:::
        [Propiedad State (ADO)](../../../ado/reference/ado-api/state-property-ado.md)  
    :::column-end:::
    :::column:::
        [State (propiedad) (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)  
    :::column-end:::
:::row-end:::

---
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
ms.openlocfilehash: b6b8c5c9a593177155f2f22d7dba4e38515e0dce
ms.sourcegitcommit: 4b775a3ce453b757c7435cc2a4c9b35d0c5a8a9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2020
ms.locfileid: "87472611"
---
# <a name="objectstateenum"></a>ObjectStateEnum
Especifica si un objeto está abierto o cerrado, se está conectando a un origen de datos, ejecutando un comando o recuperando datos.  
  
|Constante|Valor|Descripción|  
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

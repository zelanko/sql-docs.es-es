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
ms.openlocfilehash: 3f233104501a17f384eb837d5e7390705a44ddc4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762304"
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
|AdoEnums. ObjectState. EXECUTing|  
|AdoEnums. ObjectState. FETCH|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[State (propiedad) (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)|[Propiedad State (ADO)](../../../ado/reference/ado-api/state-property-ado.md)|

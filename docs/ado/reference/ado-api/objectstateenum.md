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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 41b72647af357bc73eb3e9a2f8c3063f2275f6a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66707189"
---
# <a name="objectstateenum"></a>ObjectStateEnum
Especifica si un objeto está abierto o cerrado, conectarse a un origen de datos, ejecutar un comando o la recuperación de datos.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|Indica que el objeto está cerrado.|  
|**adStateOpen**|1|Indica que el objeto está abierto.|  
|**adStateConnecting**|2|Indica que el objeto se está conectando.|  
|**adStateExecuting**|4|Indica que el objeto se está ejecutando un comando.|  
|**adStateFetching**|8|Indica que se recuperan las filas del objeto.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.ObjectState.CLOSED|  
|AdoEnums.ObjectState.OPEN|  
|AdoEnums.ObjectState.CONNECTING|  
|AdoEnums.ObjectState.EXECUTING|  
|AdoEnums.ObjectState.FETCHING|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[State (propiedad) (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)|[Propiedad State (ADO)](../../../ado/reference/ado-api/state-property-ado.md)|

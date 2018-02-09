---
title: SearchDirectionEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- SearchDirectionEnum
helpviewer_keywords:
- SearchDirectionEnum enumeration [ADO]
ms.assetid: 81272ae3-2165-4f4e-adfe-9ede0368cb17
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 46b8e127ed67c71a733cf232e92e967a031b4314
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
Especifica la dirección de una búsqueda de registros dentro de un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|Busca hacia atrás, detener al principio de la **conjunto de registros**. Si no se encuentra una coincidencia, se sitúa el puntero de registro en [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md).|  
|**adSearchForward**|1|Busca hacia adelante y detener al final de la **conjunto de registros**. Si no se encuentra una coincidencia, se sitúa el puntero de registro en [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md).|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.SearchDirection.BACKWARD|  
|AdoEnums.SearchDirection.FORWARD|  
  
## <a name="applies-to"></a>Se aplica a  
 [Find (método) (ADO)](../../../ado/reference/ado-api/find-method-ado.md)

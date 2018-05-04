---
title: ResyncEnum | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ResyncEnum
helpviewer_keywords:
- ResyncEnum enumeration [ADO]
ms.assetid: d3df2c90-e570-4c40-a79a-25b3448a009c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 79752a7733450fc1e6761f39cd49fb6f808a334b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="resyncenum"></a>ResyncEnum
Especifica si se sobrescriben los valores subyacentes por una llamada a [Resync](../../../ado/reference/ado-api/resync-method.md).  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|Predeterminado: Sobrescribe los datos y se cancelan las actualizaciones pendientes.|  
|**adResyncUnderlyingValues**|1|No sobrescribir los datos y no se cancelan las actualizaciones pendientes.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.Resync.ALLVALUES|  
|AdoEnums.Resync.UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>Se aplica a  
 [Método Resync](../../../ado/reference/ado-api/resync-method.md)

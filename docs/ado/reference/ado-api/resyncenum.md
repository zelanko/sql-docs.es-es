---
title: ResyncEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ResyncEnum
helpviewer_keywords:
- ResyncEnum enumeration [ADO]
ms.assetid: d3df2c90-e570-4c40-a79a-25b3448a009c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2bc43e772ab8f1e330d393461944cb2ecd585149
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711567"
---
# <a name="resyncenum"></a>ResyncEnum
Especifica si se sobrescriben los valores subyacentes mediante una llamada a [Resync](../../../ado/reference/ado-api/resync-method.md).  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|Predeterminado: Sobrescribe los datos y las actualizaciones pendientes se cancelan.|  
|**adResyncUnderlyingValues**|1|No sobrescribir los datos y no se cancelan las actualizaciones pendientes.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.Resync.ALLVALUES|  
|AdoEnums.Resync.UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>Se aplica a  
 [Método Resync](../../../ado/reference/ado-api/resync-method.md)

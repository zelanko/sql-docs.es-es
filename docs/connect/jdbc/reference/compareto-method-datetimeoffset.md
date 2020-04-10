---
title: Método compareTo (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e4cf2ea4-0fe9-40ce-ba79-f2a2b616997e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac80b43813106f1de991da5114b2473871222a68
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923579"
---
# <a name="compareto-method-datetimeoffset"></a>Método compareTo (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Compara este objeto **DateTimeOffset** con otro objeto **DateTimeOffset** según la hora en GMT.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int compareTo(DateTimeOffset other)  
```  
  
#### <a name="parameters"></a>Parámetros  
 Un valor [DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) que desea comparar con la instancia actual.  
  
## <a name="return-value"></a>Valor devuelto  
 La tabla siguiente describe los valores devueltos de este método:  
  
|Valor devuelto|Descripción|  
|------------------|-----------------|  
|0|Ambos objetos **DateTimeOffset** representan el mismo punto cronológico.|  
|número negativo|Este objeto **DateTimeOffset** representa un punto cronológico anterior a *other*.|  
|número positivo|Este objeto **DateTimeOffset** representa un punto cronológico posterior a *other*.|  
  
## <a name="remarks"></a>Observaciones  
 Cuando dos objetos **DateTimeOffset** tienen la misma hora de GMT, no se produce ninguna ordenación adicional de los objetos basados en el desplazamiento.  
  
## <a name="see-also"></a>Consulte también  
 [Clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Miembros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  

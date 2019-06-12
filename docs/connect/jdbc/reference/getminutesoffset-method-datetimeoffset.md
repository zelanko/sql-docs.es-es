---
title: Método getMinutesOffset (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 18ba844a-ea36-42de-87da-bbc222082efe
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6d17b5451340c07ea8c9bd0ce61bf858b419b121
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66784763"
---
# <a name="getminutesoffset-method-datetimeoffset"></a>Método getMinutesOffset (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el desplazamiento, en minutos respecto a GMT, de este objeto de DateTimeOffset.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getMinutesOffset()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 El desplazamiento en minutos.  
  
## <a name="remarks"></a>Notas  
 Para un objeto DateTimeOffset que representa el 8 de marzo de 2010, 11:35:48 -0800, getMinutesOffset devuelve el valor 480.  
  
## <a name="see-also"></a>Consulte también  
 [Clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Miembros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  

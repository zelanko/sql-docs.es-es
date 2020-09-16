---
description: Método getMinutesOffset (DateTimeOffset)
title: Método getMinutesOffset (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 18ba844a-ea36-42de-87da-bbc222082efe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a3184c0dc0389a696904386361496ea31582b0af
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435417"
---
# <a name="getminutesoffset-method-datetimeoffset"></a>Método getMinutesOffset (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el desplazamiento, en minutos, de GMT en este objeto DateTimeOffset.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getMinutesOffset()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 El desplazamiento en minutos.  
  
## <a name="remarks"></a>Observaciones  
 Para un objeto DateTimeOffset que representa el 8 de marzo de 2010, 11:35:48-0800, getMinutesOffset devuelve el valor 480.  
  
## <a name="see-also"></a>Consulte también  
 [Clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Miembros de DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  

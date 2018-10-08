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
manager: craigg
ms.openlocfilehash: b5f135ac405a5dbeda6a0c86d447e591c8bee9a1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47755343"
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
  
## <a name="see-also"></a>Ver también  
 [Clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Miembros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  

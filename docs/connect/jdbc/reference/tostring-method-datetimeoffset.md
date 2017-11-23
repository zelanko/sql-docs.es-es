---
title: "Método toString (DateTimeOffset) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e77b9be3-1a02-4769-8acf-ac71d48d6a76
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7c6dd16bfddfa331fd2647bd8fd191ac91941e71
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="tostring-method-datetimeoffset"></a>Método toString (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve una representación de cadena de la **DateTimeOffset** objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Una representación de cadena de la **DateTimeOffset** objeto.  
  
## <a name="remarks"></a>Comentarios  
 La cadena tiene el formato *aaaa*-*MM*-*DD**hh*:*mm*: *ss*[. *fffffff*] [+ |-]*hh*:*mm*.  
  
 Las fracciones de segundo de la cadena devuelta se rellenan con ceros hasta la precisión definida. Por ejemplo, un **datetimeoffset(6)** con un valor de "2010-03-10 12:34:56.78 -08:00" formateará DateTimeOffset.toString como "12:34:56.780000 2010-03-10-08:00".  
  
## <a name="see-also"></a>Vea también  
 [Clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Miembros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  

---
title: Método toString (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e77b9be3-1a02-4769-8acf-ac71d48d6a76
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 64186b6add766a21e0881fb6b3f59d49048334e8
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66778585"
---
# <a name="tostring-method-datetimeoffset"></a>Método toString (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve una representación de cadena de la **DateTimeOffset** objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Representación de cadena de la **DateTimeOffset** objeto.  
  
## <a name="remarks"></a>Notas  
 La cadena tiene el formato *aaaa*-*MM*-*DD ** hh*:*mm*:*ss*[. *fffffff*] [+ |-]*hh*:*mm*.  
  
 Las fracciones de segundo de la cadena devuelta se rellenan con ceros hasta la precisión definida. Por ejemplo, un **datetimeoffset(6)** con un valor de "2010-03-10 12:34:56.78 -08:00" formateará DateTimeOffset.toString como "12:34:56.780000 2010-03-10-08:00".  
  
## <a name="see-also"></a>Consulte también  
 [Clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Miembros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  

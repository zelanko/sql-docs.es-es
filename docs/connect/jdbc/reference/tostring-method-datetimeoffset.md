---
title: toString (método) (DateTimeOffset) | Microsoft Docs
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
ms.openlocfilehash: ef3cd31068c324475e8edfe8bf8f7c16acc4a2de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67968513"
---
# <a name="tostring-method-datetimeoffset"></a>Método toString (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve una representación de cadena del objeto **DateTimeOffset** .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Representación de cadena del objeto **DateTimeOffset** .  
  
## <a name="remarks"></a>Notas  
 La cadena tiene el formato *AAAA*-*mm*-*DD * * HH*:*mm*:*SS*[. *FFFFFFF*] [+ |-]*HH*:*mm*.  
  
 Las fracciones de segundo de la cadena devuelta se rellenan con ceros hasta la precisión definida. Por ejemplo, DateTimeOffset. toString dará formato a **DateTimeOffset (6)** con un valor de "2010-03-10 12:34:56.78-08:00" como "2010-03-10 12:34:56.780000-08:00".  
  
## <a name="see-also"></a>Consulte también  
 [Clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Miembros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  

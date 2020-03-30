---
title: Método setAsciiStream (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 617ece92-0fb1-4f95-b32d-29b5b56eb3fb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 043a94108bdb7c8938f06e8bf1d4bf58651fbf21
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67975368"
---
# <a name="setasciistream-method-sqlservernclob"></a>Método setAsciiStream (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera un flujo que se va a utilizar para escribir caracteres ASCII para el valor **NCLOB** que representa este objeto **java.sql.NClob**, a partir de la posición especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.io.OutputStream setAsciiStream(long pos)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *pos*  
  
 La posición en la que se comienza a escribir en el objeto **NCLOB**; la primera posición es 1.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto OutputStream que representa el flujo en el que se pueden escribir caracteres ASCII codificados.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método setAsciiStream especifica este método setAsciiStream en la interfaz java.sql.NClob.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Miembros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Clase SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  

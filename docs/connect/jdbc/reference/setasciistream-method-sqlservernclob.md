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
manager: jroth
ms.openlocfilehash: aebc713ab5256527571eb1a4277caa74e53623d7
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66765049"
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
  
## <a name="remarks"></a>Notas  
 Este método setAsciiStream especificado por el método setAsciiStream en la interfaz java.sql.NClob.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Miembros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Clase SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  

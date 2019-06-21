---
title: Método setCharacterStream (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 09042ee9-dfb1-4d0b-82bd-d1224b0aea80
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: dbddcadfec0ed7b2bab9573717d0079240443a94
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66795693"
---
# <a name="setcharacterstream-method-sqlservernclob"></a>Método setCharacterStream (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera un flujo que se va a utilizar para escribir un flujo de Unicode para el valor **NCLOB** que representa este objeto **Java.sql.NClob**, a partir de la posición especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.io.Writer setCharacterStream(long pos)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *pos*  
  
 La posición en la que se comienza a escribir en el valor **NCLOB**; la primera posición es 1.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto Writer que representa el flujo en el que se pueden escribir caracteres Unicode codificados.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método setCharacterStream especificado por el método setCharacterStream en la interfaz java.sql.NClob.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Miembros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Clase SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  

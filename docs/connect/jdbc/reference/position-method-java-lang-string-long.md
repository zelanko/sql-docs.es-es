---
title: Método Position (java.lang.String, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.position (java.lang.String, long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 86fad8ed-375a-42e1-b40e-1fa085957a2c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 40c7dadf83861d889acd7932dbe1dad17fda4b35
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802451"
---
# <a name="position-method-javalangstring-long"></a>Método position (java.lang.String, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve la posición de un carácter de la subcadena especificada en el CLOB según la posición de inicio determinada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public long position(java.lang.String searchstr,  
                     long start)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *searchstr*  
  
 La subcadena que se va a buscar.  
  
 *start*  
  
 La posición donde se empieza la búsqueda; la primera posición es 1.  
  
## <a name="return-value"></a>Valor devuelto  
 La posición donde aparece la subcadena o -1 si no está presente; la primera posición es 1.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método de posición se especifica el método de posición en la interfaz java.sql.Clob.  
  
## <a name="see-also"></a>Consulte también  
 [Método Position &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/position-method-sqlserverclob.md)   
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Miembros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Clase SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  

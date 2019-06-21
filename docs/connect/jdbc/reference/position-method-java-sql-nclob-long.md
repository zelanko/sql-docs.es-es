---
title: Método Position (java.sql.NClob, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f2354278-d128-4cf4-a170-22c05fcb763b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 35d8a3903cc18ce371b2d6c333747710ac6efc7e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802423"
---
# <a name="position-method-javasqlnclob-long"></a>Método position (java.sql.NClob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera la posición del carácter en el que el especificado **NClob** objeto *searchstr* aparece en este **NClob** objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
long position(java.sql.NClob searchstr,  
              long start)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *searchstr*  
  
 Un objeto NClob que se va a buscar.  
  
 *start*  
  
 La posición donde se empieza la búsqueda; la primera posición es 1.  
  
## <a name="return-value"></a>Valor devuelto  
 La posición donde aparece la subcadena o -1 si no está presente. La primera posición es 1.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método de posición se especifica el método de posición en la interfaz java.sql.NClob.  
  
## <a name="see-also"></a>Consulte también  
 [Método Position &#40;SQLServerNClob&#41;](../../../connect/jdbc/reference/position-method-sqlservernclob.md)   
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Miembros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Clase SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  

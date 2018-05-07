---
title: Método setString (long, java.lang.String) - NClob | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 698073b2-3f0c-449c-ad68-48144698fe8f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fc953a2026bf4fca9401b1eb9484ff9f34435e2e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="setstring-method-long-javalangstring-sqlservernclob"></a>Método setString (long, java.lang.String) (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Escribe el determinado **cadena** a la **NCLOB** a partir de la posición especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int setString(long pos,  
              java.lang.String str)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *punto de venta*  
  
 La posición donde se comienza a escribir en el **NCLOB**; la primera posición es 1.  
  
 *str*  
  
 La cadena se escriban en el **NCLOB**.  
  
## <a name="return-value"></a>Valor devuelto  
 El número de caracteres que se han escrito.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setString especificado por el método setString en la interfaz java.sql.NClob.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Miembros de SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Clase SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  

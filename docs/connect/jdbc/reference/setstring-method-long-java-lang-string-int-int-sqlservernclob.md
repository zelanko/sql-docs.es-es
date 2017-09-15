---
title: "Método setString (long, java.lang.String, int, int) - NClob | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2d5e9f50-15b2-4c76-8bfc-3b5be49c2781
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d09ee2a09d313a192d30dc09ff07f4f3bd35d499
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setstring-method-long-javalangstring-int-int-sqlservernclob"></a>Método setString (long, java.lang.String, int, int) (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Escribe la cadena especificada en el NCLOB comenzando en la posición especificada, basándose en el desplazamiento y longitud indicados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
int setString(long pos,  
              java.lang.String str,  
              int offset,  
              int len)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *punto de venta*  
  
 La posición donde se comienza a escribir en el **NCLOB**; la primera posición es 1.  
  
 *str*  
  
 La cadena se escriban en el **NCLOB**.  
  
 *desplazamiento*  
  
 Desplazamiento en *str* para empezar a leer los caracteres que se va a escribir.  
  
 *Len*  
  
 El número de caracteres que se va a escribir.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setString especificado por el método setString en la interfaz java.sql.NClob.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Miembros de SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Clase SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  

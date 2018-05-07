---
title: Método setString (long, java.lang.String) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerClob.setString (long, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1b2190e9-5ace-497a-8554-0e913ea9b0cb
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7194a8778ecae136d7a70086c5fa2e9353988a93
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="setstring-method-long-javalangstring"></a>Método setString (long, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Escribe el determinado **cadena** en el objeto CLOB a partir de la posición especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int setString(long pos,  
                     java.lang.String s)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *punto de venta*  
  
 La posición donde se comienza a escribir en el CLOB.  
  
 *S*  
  
 El **cadena** se escriban en el objeto CLOB.  
  
## <a name="return-value"></a>Valor devuelto  
 El número de caracteres que se han escrito.  
  
## <a name="exceptions"></a>Excepciones  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentarios  
 Este método setString especificado por el método setString en la interfaz java.sql.Clob.  
  
 Los datos de caracteres se sobrescriben tomando como punto de inicio la posición especificada y pueden saturar la longitud inicial del CLOB. Si se especifica un valor position+1, se anexará la cadena. Si especifica valores de position+2 o superiores (o cero o menos), producirán un error de la posición.  
  
## <a name="see-also"></a>Vea también  
 [Método setString &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/setstring-method-sqlserverclob.md)   
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Miembros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Clase SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  

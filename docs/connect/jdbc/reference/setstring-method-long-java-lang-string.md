---
title: Método setString (long, java.lang.String, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.setString (long, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1b2190e9-5ace-497a-8554-0e913ea9b0cb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b23c0c5de87fc5df557d5d02958a72eaa336f8fb
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66771669"
---
# <a name="setstring-method-long-javalangstring"></a>Método setString (long, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Escribe el objeto **String** especificado en el CLOB a partir de la posición determinada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int setString(long pos,  
                     java.lang.String s)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *pos*  
  
 La posición donde se comienza a escribir en el CLOB.  
  
 *s*  
  
 El objeto **String** que se va a escribir en CLOB.  
  
## <a name="return-value"></a>Valor devuelto  
 El número de caracteres que se han escrito.  
  
## <a name="exceptions"></a>Excepciones  
 java.sql.SQLException  
  
## <a name="remarks"></a>Notas  
 El método setString especifica este método setString en la interfaz java.sql.CallableStatement.  
  
 Los datos de caracteres se sobrescriben tomando como punto de inicio la posición especificada y pueden saturar la longitud inicial del CLOB. Si se especifica un valor position+1, se anexará la cadena. Si especifica valores de position+2 o superiores (o cero o menos), producirán un error de la posición.  
  
## <a name="see-also"></a>Consulte también  
 [Método setString &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/setstring-method-sqlserverclob.md)   
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Miembros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Clase SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  

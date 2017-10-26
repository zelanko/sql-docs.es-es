---
title: "Método getCharacterStream (long, long) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d70f502f-f60f-436a-83e6-797a0ed71bf3
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ba910c36ff82209a668ef6d96987330705703080
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getcharacterstream-method-long-long"></a>Método getCharacterStream (long, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el **Clob** datos como un objeto de lector o como una secuencia de caracteres con la posición y longitud especificadas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.io.Reader getCharacterStream(long pos,  
                                         long length)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *punto de venta*  
  
 A **largo** que indica el desplazamiento hasta el primer carácter del valor parcial que se va a recuperar.  
  
 *length*  
  
 A **largo** que indica la longitud en caracteres del valor parcial que se va a recuperar.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto de lector que contiene el **Clob** datos.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getCharacterStream especificado por el método getCharacterStream en la interfaz java.sql.Clob.  
  
## <a name="see-also"></a>Vea también  
 [Método getCharacterStream &#40; SQLServerClob &#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverclob.md)   
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Miembros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)  
  
  


---
title: Método getCharacterStream (long, long) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d70f502f-f60f-436a-83e6-797a0ed71bf3
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea78140d5a0bd24a71d9ab4c846ded3e74822f18
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32830700"
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
 [Método getCharacterStream &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverclob.md)   
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Miembros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)  
  
  

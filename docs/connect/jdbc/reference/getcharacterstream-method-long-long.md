---
title: Método getCharacterStream (long, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d70f502f-f60f-436a-83e6-797a0ed71bf3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a47b7ea56873b0b502ba39a91e4d1ba30044e993
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67953255"
---
# <a name="getcharacterstream-method-long-long"></a>Método getCharacterStream (long, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve los datos de **Clob** como un objeto Reader o como un flujo de caracteres con la posición y longitud especificadas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.io.Reader getCharacterStream(long pos,  
                                         long length)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *pos*  
  
 Un valor **long** que indica el desplazamiento al primer carácter del valor parcial que se va a recuperar.  
  
 *length*  
  
 Un valor **long** que indica la longitud en caracteres del valor parcial que se va a recuperar.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto Reader que contiene los datos **Clob**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getCharacterStream especifica este método getCharacterStream en la interfaz java.sql.Clob.  
  
## <a name="see-also"></a>Consulte también  
 [Método getCharacterStream &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverclob.md)   
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Miembros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)  
  
  

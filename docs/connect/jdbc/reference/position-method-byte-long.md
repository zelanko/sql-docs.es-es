---
title: Método Position (byte, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.position (byte[], long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 787412c2-4342-49c8-9ca2-7a9ddcd3277c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e6056412f6ab2726112d5286f2f52c83ff6691cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802469"
---
# <a name="position-method-byte-long"></a>Método position (byte, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve la posición de un patrón especificado en el BLOB según el patrón de matriz **byte** determinado y el índice de inicio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public long position(byte[] bPattern,  
                     long start)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *bPattern*  
  
 El modelo que se va a buscar.  
  
 *start*  
  
 El índice inicial que se va a buscar.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **long** de la posición en la que se encontró el modelo; en caso de no encontrarse, el valor es -1.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método de posición se especifica el método de posición en la interfaz java.sql.Blob.  
  
## <a name="see-also"></a>Consulte también  
 [Método Position &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/position-method-sqlserverblob.md)   
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Miembros SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Clase SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  

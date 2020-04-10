---
title: Método position (byte, long) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 938254b8076d78ebd1ac768d130904077828aa03
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80914391"
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
  
## <a name="remarks"></a>Observaciones  
 El método position especifica este método position en la interfaz java.sql.Blob.  
  
## <a name="see-also"></a>Consulte también  
 [Método position &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/position-method-sqlserverblob.md)   
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Miembros SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Clase SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  

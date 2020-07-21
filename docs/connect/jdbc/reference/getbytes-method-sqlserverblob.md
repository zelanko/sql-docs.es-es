---
title: Método getBytes (SQLServerBlob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.getBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bea1b810-b5c1-466d-bdc4-561468214632
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 00ae9db184a8fa8818f93402551a58580a9b833b
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921584"
---
# <a name="getbytes-method-sqlserverblob"></a>Método getBytes (SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Obtiene los datos Blob como una matriz de bytes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public byte[] getBytes(long pos,  
                       int length)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *pos*  
  
 Posición inicial; comienza en 1 (no en 0).  
  
 *length*  
  
 Longitud de los datos que se van a obtener.  
  
## <a name="return-value"></a>Valor devuelto  
 Una matriz de **byte** que contiene los datos que se han solicitado.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getBytes especifica este método getBytes en la interfaz java.sql.Blob.  
  
 Si la longitud del objeto BLOB es NULL o cero y se intentan obtener cero bytes exactamente en la posición 1, se devuelve una matriz de **byte** vacía (matriz de bytes de longitud 0).  
  
 Si el valor del objeto BLOB es NULL o tiene longitud cero y se intenta obtener una longitud de bytes determinada en una posición que no sea 1, se producirá una excepción relativa a la posición.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Miembros SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Clase SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  

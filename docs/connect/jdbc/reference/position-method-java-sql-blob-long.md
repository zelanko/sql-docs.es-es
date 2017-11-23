---
title: "Método Position (java.sql.Blob, long) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerBlob.position (java.sql.Blob.long)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: ebd005e5-f6c5-4789-87f9-d2fdacd35060
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a6289e392663ccd3d5bf25c94e7162bfe507630d
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="position-method-javasqlblob-long"></a>Método position (java.sql.Blob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve la posición de un patrón especificado en el BLOB según el patrón determinado y el índice de inicio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public long position(java.sql.Blob pattern,  
                     long start)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *patrón*  
  
 El modelo que se va a buscar.  
  
 *Inicio*  
  
 El índice inicial que se va a buscar.  
  
## <a name="return-value"></a>Valor devuelto  
 A **largo** valor de la posición donde se encuentra el patrón, o -1 si no se encontró.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método de posición se especifica el método de posición en la interfaz java.sql.Blob.  
  
## <a name="see-also"></a>Vea también  
 [Coloque el método &#40; SQLServerBlob &#41;](../../../connect/jdbc/reference/position-method-sqlserverblob.md)   
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Miembros de SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Clase SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  

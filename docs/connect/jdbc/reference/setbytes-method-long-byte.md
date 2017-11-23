---
title: "setBytes (método) (long, byte) | Documentos de Microsoft"
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
apiname: SQLServerBlob.setBytes (long.byte[])
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: ffb8f107-0f9d-4410-957f-62b718e1e872
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e554122e5435a42f3c35c9a94904c6a329b23e82
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="setbytes-method-long-byte"></a>setBytes (long, byte) (método)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Escribe la matriz de bytes determinada en el BLOB comenzando en la posición determinada y posteriormente devuelve el número de bytes escritos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int setBytes(long pos,  
                    byte[] bytes)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *punto de venta*  
  
 La posición (basado en 1) en el BLOB en la que se va a empezar a escribir los datos.  
  
 *bytes*  
  
 La matriz de bytes que se va a escribir en el BLOB.  
  
## <a name="return-value"></a>Valor devuelto  
 A **largo** valor que especifica el número de bytes escritos.  
  
## <a name="exceptions"></a>Excepciones  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentarios  
 Este método setBytes es especificado por el método setBytes en la interfaz java.sql.Blob.  
  
 Los datos se sobrescriben tomando como punto de inicio la posición especificada y pueden saturar la longitud inicial del BLOB. Si se especifican valores position+1, se anexarán bytes. Si se pasan valores position+2 o superiores (o cero o menos), se producirá un error de la posición. Pasar una longitud de cero **bytes** matriz devolverá cero porque no se escribieron bytes.  
  
## <a name="see-also"></a>Vea también  
 [Método setBytes &#40; SQLServerBlob &#41;](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)   
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Miembros de SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Clase SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  

---
description: Método position (java.sql.Clob, long)
title: Método position (java.sql.Clob, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.position (java.sql.Clob, long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b2fb34d5-1d34-4764-a795-712d9c6aa313
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d782839bc1a68008c4e86231fdf436b8c6f7a580
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433027"
---
# <a name="position-method-javasqlclob-long"></a>Método position (java.sql.Clob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve la posición de un carácter del objeto CLOB especificado en el CLOB según la posición de inicio determinada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public long position(java.sql.Clob searchstr,  
                     long start)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *searchstr*  
  
 Subcadena para buscar.  
  
 *start*  
  
 La posición donde se empieza la búsqueda. La primera posición es 1.  
  
## <a name="return-value"></a>Valor devuelto  
 La posición donde aparece la subcadena o -1 si no está presente. La primera posición es 1.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método position especifica este método position en la interfaz java.sql.Clob.  
  
## <a name="see-also"></a>Consulte también  
 [Método position &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/position-method-sqlserverclob.md)   
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Miembros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Clase SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  

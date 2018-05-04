---
title: parámetro de método (java.lang.String) getDate | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getDate (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a605bca6-d960-4756-ad14-0f42b313e60a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 004e82182e71cb1f37f466cc89e86eb0a0399ba9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getdate-method-javalangstring"></a>Método getDate (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto java.sql.Date en el lenguaje de programación Java según el nombre de parámetro especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Date getDate(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 A **cadena** que contiene el nombre del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto de fecha.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getDate es especificado por el método getDate en la interfaz java.sql.CallableStatement.  
  
 Este método devuelve una parte de fecha válida de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **datetime** o **smalldatetime** tipo de datos, con la parte de hora establecida en la hora de inicio de Java de 00:00 (medianoche).  
  
## <a name="see-also"></a>Vea también  
 [Método getDate &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdate-method-sqlservercallablestatement.md)   
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

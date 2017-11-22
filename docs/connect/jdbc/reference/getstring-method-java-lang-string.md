---
title: "Método getString (java.lang.String) | Documentos de Microsoft"
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
apiname: SQLServerCallableStatement.getString (java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: f67371e0-e879-4188-85fc-ecb85f0be2a9
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e6d9437a7fbba96fc92908fdd875dae964ee3bbb
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="getstring-method-javalangstring"></a>Método getString (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un **cadena** en el lenguaje de según el nombre del parámetro de programación Java.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getString(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 A **cadena** que contiene el nombre del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 A **cadena** valor.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getString especificado por el método getString de la interfaz java.sql.CallableStatement.  
  
 Todas las columnas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] puede devolverse como una cadena. Lo cual indica que se puede devolver una representación de cadena de todos los tipos basados en número y en caracteres y una representación de una cadena hexadecimal de columnas binarias como binary, varbinary, varbinary(max), image, timestamp y uniqueidentifier.  
  
 Tipos de dependientes de la ubicación como money, smallmoney, datetime, smalldatetime, float, real, decimal y numeric devolverán el formato canónico toString() para el valor subyacente del tipo.  
  
 Los tipos definidos por el usuario se devuelven como valores de cadena.  
  
## <a name="see-also"></a>Vea también  
 [Método getString &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getstring-method-sqlservercallablestatement.md)   
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

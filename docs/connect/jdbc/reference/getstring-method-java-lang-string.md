---
title: Método getString (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getString (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f67371e0-e879-4188-85fc-ecb85f0be2a9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 114eaa8b3300f5e0785a3bac389eb00d4d5ee7ec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66773727"
---
# <a name="getstring-method-javalangstring"></a>Método getString (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto **String** en el lenguaje de programación Java según el nombre del parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getString(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 Objeto **String** que contiene el nombre del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **String**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método getString especifica este método getString en la interfaz java.sql.CallableStatement.  
  
 Todas las columnas en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se pueden devolver como una cadena. Lo cual indica que se puede devolver una representación de cadena de todos los tipos basados en número y en caracteres y una representación de una cadena hexadecimal de columnas binarias como binary, varbinary, varbinary(max), image, timestamp y uniqueidentifier.  
  
 Los tipos importantes para la ubicación como money, smallmoney, datetime, smalldatetime, float, real, decimal y numeric devolverán el formato canónico toString() para el valor subyacente del tipo.  
  
 Los tipos definidos por el usuario se devuelven como valores de cadena.  
  
## <a name="see-also"></a>Consulte también  
 [Método getString &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getstring-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

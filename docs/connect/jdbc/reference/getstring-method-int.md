---
title: Método getString (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getString (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f3fce8bf-8d6e-476f-aa6d-992daa79b899
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 92257f0941b34ffdf108b10debad55ce7532b98d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66773861"
---
# <a name="getstring-method-int"></a>Método getString (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto **String** en el lenguaje de programación Java según el índice del parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getString(int index)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *index*  
  
 Un valor **int** que indica el índice del parámetro.  
  
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
  
  

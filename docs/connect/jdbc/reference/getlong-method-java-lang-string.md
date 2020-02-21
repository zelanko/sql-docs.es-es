---
title: Método getLong (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getLong (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 92e30537-5fd9-4b67-8b0f-486c6e840e03
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dd7081c6ece290be866b395388ae28ee8b56b312
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67982444"
---
# <a name="getlong-method-javalangstring"></a>Método getLong (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto **long** en el lenguaje de programación Java según el nombre de parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public long getLong(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 Objeto **String** que contiene el nombre del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **long**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getLong especifica este método getLong en la interfaz java.sql.CallableStatement.  
  
 Este método solamente se admite en los tipos de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que pueden devolver de forma segura un valor entero como **bigint**, **int**, **smallint**, **tinyint** y **bit**. Si se utiliza este método en cualquier otro tipo de datos, provocará una excepción.  
  
## <a name="see-also"></a>Consulte también  
 [Método getLong &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getlong-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

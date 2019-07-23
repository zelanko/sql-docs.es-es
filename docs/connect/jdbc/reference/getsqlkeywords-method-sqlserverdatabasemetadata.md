---
title: Método getSQLKeywords (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSQLKeywords
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a2a0dfbb-11ec-429f-aea6-8f44148ebb8e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 79995b672219c456284809ee16593fbe800a9638
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979743"
---
# <a name="getsqlkeywords-method-sqlserverdatabasemetadata"></a>Método getSQLKeywords (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una lista separada por comas de las palabras clave de SQL de toda esta base de datos que sean también palabras clave de SQL92.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getSQLKeywords()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto **String** que contiene las palabras clave SQL.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getSQLKeywords se especifica mediante el método getSQLKeywords en la interfaz java. SQL. DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

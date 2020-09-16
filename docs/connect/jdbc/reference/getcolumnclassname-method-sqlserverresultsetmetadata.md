---
description: Método getColumnClassName (SQLServerResultSetMetaData)
title: Método getColumnClassName (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.getColumnClassName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2c118790-5dd2-4b10-93b6-7f065ee324ce
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 143522437983b6e1d82ef8e617dbbb2ad7bd0222
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436597"
---
# <a name="getcolumnclassname-method-sqlserverresultsetmetadata"></a>Método getColumnClassName (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el nombre completo de la clase Java cuyas instancias se generan si se llama al método [getObject](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md) de la clase [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) para que recupere un valor en la columna.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getColumnClassName(int column)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *column*  
  
 Valor **int** que indica el índice de la columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **String** que contiene el nombre completo de la clase.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getColumnClassName especifica este método getColumnClassName en la interfaz java.sql.ResultSetMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [Miembros SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Clase SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  

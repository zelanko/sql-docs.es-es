---
description: Método getTime (java.lang.String) (SQLServerResultSet)
title: Método getTime (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getTime (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e0efc0b3-4da4-45fc-9e8d-5edd9da7a42d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a7c4d054b6ea5fa5983a149bce2c1319180f9785
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434197"
---
# <a name="gettime-method-javalangstring-sqlserverresultset"></a>Método getTime (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del nombre de la columna designada en la fila actual de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como un objeto java.sql.Time en el lenguaje de programación Java.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Time getTime(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnName*  
  
 Valor **String** que contiene el nombre de columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto Time.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getTime especifica este método getTime en la interfaz java.sql.ResultSet.  
  
 Este método devuelve una hora válida que forma parte de un tipo de datos datetime o smalldatetime de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], con la parte correspondiente a la fecha establecida en la fecha de inicio de Java de 1970/01/01.  
  
## <a name="see-also"></a>Consulte también  
 [Método getTime &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/gettime-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

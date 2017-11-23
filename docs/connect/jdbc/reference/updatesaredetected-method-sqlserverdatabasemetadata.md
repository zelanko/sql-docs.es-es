---
title: "Método updatesAreDetected (SQLServerDatabaseMetaData) | Documentos de Microsoft"
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
apiname: SQLServerDatabaseMetaData.updatesAreDetected
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: cb541175-d3a5-4bca-b327-64e2270c0df1
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 30886e3c395178ac59eb29dffb1197dfb124d133
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="updatesaredetected-method-sqlserverdatabasemetadata"></a>Método updatesAreDetected (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si no se puede detectar una actualización de filas visible mediante una llamada a la [rowUpdated](../../../connect/jdbc/reference/rowupdated-method-sqlserverresultset.md) método de la [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) clase.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean updatesAreDetected(int type)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Tipo*  
  
 Un **int** que indica el conjunto de resultados tipo, que puede ser uno de los siguientes valores tal como se define en java.sql.ResultSet o SQLServerResultSet:  
  
## <a name="javasqlresultset-types"></a>Tipos java.sql.ResultSet  
 TYPE_FORWARD_ONLY  
  
 TYPE_SCROLL_SENSITIVE  
  
 TYPE_SCROLL_INSENSITIVE  
  
## <a name="sqlserverresultset-types"></a>Tipos SQLServerResultSet  
 TYPE_SS_SCROLL_STATIC  
  
 TYPE_SS_SCROLL_KEYSET  
  
 TYPE_SS_DIRECT_FORWARD_ONLY  
  
 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY  
  
 TYPE_SS_SCROLL_DYNAMIC  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si se puede detectar la actualización de filas. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método updatesAreDetected especificado por el método updatesAreDetected en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

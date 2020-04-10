---
title: Método supportsResultSetConcurrency (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsResultSetConcurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8f7573b2-ac5c-4721-8a02-4b6cb60c74b2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 067809bbd5bad3933dd3e7e66f538663ceb4e103
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919970"
---
# <a name="supportsresultsetconcurrency-method-sqlserverdatabasemetadata"></a>Método supportsResultSetConcurrency (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos admite el tipo de simultaneidad determinado en combinación con el tipo de conjunto de resultados determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsResultSetConcurrency(int type,  
                                            int concurrency)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *type*  
  
 Un valor **int** que indica el tipo de conjunto de resultados, que puede ser uno de los siguientes valores como queda definido en java.sql.ResultSet o SQLServerResultSet:  
  
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
  
 *concurrency*  
  
 Un valor **int** que indica el nivel de simultaneidad del conjunto de resultados, el cual puede ser uno de los siguientes valores tal como quede definido en java.sql.ResultSet o SQLServerResultSet:  
  
## <a name="javasqlresultset-types"></a>Tipos java.sql.ResultSet  
 CONCUR_READ_ONLY  
  
 CONCUR_UPDATABLE  
  
## <a name="sqlserverresultset-types"></a>Tipos SQLServerResultSet  
 CONCUR_SS_OPTIMISTIC_CC  
  
 CONCUR_SS_SCROLL_LOCKS  
  
 CONCUR_SS_OPTIMISTIC_VAL  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si es compatible. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método supportsResultSetConcurrency especifica este método supportsResultSetConcurrency en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

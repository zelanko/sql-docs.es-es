---
description: Método isCaseSensitive (SQLServerResultSetMetaData)
title: Método isCaseSensitive (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.isCaseSensitive
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4db67eb7-7ff2-4fb8-8052-39f699de53ff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9145453ef1b483f554e3c27599415021c5295b6e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433627"
---
# <a name="iscasesensitive-method-sqlserverresultsetmetadata"></a>Método isCaseSensitive (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica si la columna distingue mayúsculas de minúsculas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean isCaseSensitive(int column)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *column*  
  
 Valor **int** que indica el índice de la columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Es **true** si la columna distingue mayúsculas de minúsculas. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método isCaseSensitive especifica este método isCaseSensitive en la interfaz java.sql.ResultSetMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [Miembros SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Clase SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  

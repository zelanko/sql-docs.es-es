---
title: Método prepareCall (java.lang.String, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareCall (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 04d36a25-7f95-4675-9690-4462671b3d67
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7b51cbe470169459469959448208b3aa53b18cce
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67976254"
---
# <a name="preparecall-method-javalangstring-int-int"></a>Método prepareCall (java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Crea un objeto [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) que genera objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) con el tipo y simultaneidad especificados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql,  
                                              int resultSetType,  
                                              int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sql*  
  
 Un valor **String** que contiene la instrucción SQL.  
  
 *resultSetType*  
  
 Un valor **int** que indica el tipo de conjunto de resultados.  
  
 *resultSetConcurrency*  
  
 Un valor **int** que indica el tipo de simultaneidad del conjunto de resultados.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto CallableStatement.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método prepareCall especifica este método prepareCall en la interfaz java.sql.Connection.  
  
## <a name="see-also"></a>Consulte también  
 [Método prepareCall &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

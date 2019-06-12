---
title: Método prepareStatement (java.lang.String, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5bb96dbe-f673-41b5-911b-8f661cca071a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0cfbcf94a1211738b0cf0abb8e2657257edd09eb
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796705"
---
# <a name="preparestatement-method-javalangstring-int-int"></a>Método prepareStatement (java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Crea un objeto [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) que genera objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) con el tipo y simultaneidad especificados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.PreparedStatement prepareStatement(java.lang.String sSql,  
                                                   int resultSetType,  
                                                   int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sSql*  
  
 Un valor **String** que contiene la instrucción SQL.  
  
 *resultSetType*  
  
 Un valor **int** que indica el tipo de conjunto de resultados.  
  
 *resultSetConcurrency*  
  
 Un valor **int** que indica el tipo de simultaneidad del conjunto de resultados.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto PreparedStatement.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método prepareStatement especificado por el método prepareStatement en la interfaz java.sql.Connection.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-methods.md)   
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

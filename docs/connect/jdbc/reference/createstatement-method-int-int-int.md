---
title: Método createStatement (int, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.createStatement (int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2e4fa385-8f61-4394-8f75-3e839930a57d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 99d01841ca24cc1a7e34864b42018dac51fa1861
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66768232"
---
# <a name="createstatement-method-int-int-int"></a>Método createStatement (int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Crea un objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) que genera objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) con el tipo, simultaneidad y capacidad de alojamiento especificados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Statement createStatement(int nType,  
                                          int nConcur,  
                                          int nHold)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *resultSetType*  
  
 El **int** valor que representa el resultado de establece el tipo.  
  
 *nConcur*  
  
 El valor **int** que representa el tipo de simultaneidad del conjunto de resultados.  
  
 *nHold*  
  
 El valor **int** que representa la capacidad de alojamiento.  
  
## <a name="return-value"></a>Valor devuelto  
 El objeto de instrucción.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método createStatement especificado por el método createStatement de la interfaz java.sql.Connection.  
  
## <a name="see-also"></a>Consulte también  
 [Método createStatement &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

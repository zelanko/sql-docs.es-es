---
title: Método setHoldability (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setHoldability
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 552eebd0-4c38-43f0-961f-35244f99109b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fe53c38e1b3f1633be27f4c82a9c2edfe9820495
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68213668"
---
# <a name="setholdability-method-sqlserverconnection"></a>Método setHoldability (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cambia la capacidad de alojamiento de los objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) que se han creado mediante el uso de este objeto [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) según la capacidad de alojamiento determinada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setHoldability(int nNewHold)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *nNewHold*  
  
 Un valor **int** que contiene uno de los siguientes niveles capacidad de alojamiento:  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método setHoldability se especifica mediante el método setHoldability en la interfaz java. SQL. Connection.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

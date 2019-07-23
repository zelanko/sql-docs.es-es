---
title: Método setServerPreparedStatementDiscardThreshold (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8f66746b15e96f49d96b428e8cf8844eeea12a12
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972922"
---
# <a name="setserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>Método setServerPreparedStatementDiscardThreshold (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Especifica el comportamiento de una instancia de conexión concreta. Esta configuración controla el número de acciones de descarte de instrucciones preparada pendientes (sp_unprepare) que pueden quedar pendientes por conexión antes de que se ejecute una llamada para limpiar los controladores pendientes en el servidor. Cuando el valor es < = 1 las acciones de despreparar se ejecutan inmediatamente en el cierre de la instrucción preparada. Si el valor se establece en > 1, estas llamadas se agrupan por lotes para evitar la sobrecarga de llamar a sp_unprepare con demasiada frecuencia.


## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setServerPreparedStatementDiscardThreshold(boolean thresholdValue)  
```  

#### <a name="parameters"></a>Parámetros  
 *thresholdValue*  
 
 Nuevo valor de la propiedad de conexión **serverPreparedStatementDiscardThreshold** .  
 
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Notas  
 Este método está disponible en la versión 6,4 y posteriores del controlador JDBC.
 
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

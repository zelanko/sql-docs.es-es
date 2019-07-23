---
title: Método getServerPreparedStatementDiscardThreshold (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 87d7f85799524e3ac7c0e4d99608ce1d82b8f2fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979932"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>Método getServerPreparedStatementDiscardThreshold (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Devuelve el valor de la propiedad de conexión **serverPreparedStatementDiscardThreshold** . Esta configuración controla el número de acciones de descarte de instrucciones preparada pendientes (sp_unprepare) que pueden quedar pendientes por conexión antes de que se ejecute una llamada para limpiar los controladores pendientes en el servidor. Si el valor es < = 1, las acciones de despreparar se ejecutan inmediatamente en el cierre de la instrucción preparada. Si se establece en > 1, estas llamadas se agrupan por lotes para evitar la sobrecarga de llamar a sp_unprepare con demasiada frecuencia. El valor predeterminado de esta opción se puede cambiar mediante una llamada a getDefaultServerPreparedStatementDiscardThreshold ().

## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getServerPreparedStatementDiscardThreshold()  
```  

## <a name="return-value"></a>Valor devuelto
 **Entero** que contiene el valor de la propiedad de conexión **serverPreparedStatementDiscardThreshold** .

## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Notas  
 Este método está disponible en la versión 6,4 y posteriores del controlador JDBC.
 
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

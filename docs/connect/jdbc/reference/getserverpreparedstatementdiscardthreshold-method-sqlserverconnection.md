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
manager: craigg
ms.openlocfilehash: dd78992abf04f78bb7b8fe879d030e906568588c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47638697"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>Método getServerPreparedStatementDiscardThreshold (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Devuelve el valor de **valor de serverPreparedStatementDiscardThreshold** propiedad de conexión. Esta configuración controla cuántos pendientes preparado descarte instrucción acciones (sp_unprepare) pueden estar pendientes por conexión antes de que se ejecuta una llamada para limpiar los controladores pendientes en el servidor. Si el valor es < = 1, unprepare acciones se ejecutan inmediatamente en la instrucción preparada cierre. Si se establece en > 1, estas llamadas se procesan por lotes juntos para evitar una sobrecarga de la llamada a sp_unprepare con demasiada frecuencia. El valor predeterminado para esta opción se puede cambiar por getDefaultServerPreparedStatementDiscardThreshold() que realiza la llamada.

## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getServerPreparedStatementDiscardThreshold()  
```  

## <a name="return-value"></a>Valor devuelto
 Un **int** que contiene el valor de **valor de serverPreparedStatementDiscardThreshold** propiedad de conexión.

## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Notas  
 Este método está disponible desde la versión del controlador JDBC 6.4 y en marcha.
 
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

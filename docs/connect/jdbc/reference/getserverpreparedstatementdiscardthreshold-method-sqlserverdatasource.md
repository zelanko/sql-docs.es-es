---
title: Método getServerPreparedStatementDiscardThreshold (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3f91b75b5c70029d53582b8b6ed4655485fd3fcf
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67979907"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverdatasource"></a>Método getServerPreparedStatementDiscardThreshold (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el valor de la propiedad de conexión **serverPreparedStatementDiscardThreshold**. Este valor controla cuántas acciones de descarte de instrucción preparada pendientes (sp_unprepare) pueden estar pendientes por conexión antes de que se ejecute una llamada para limpiar los identificadores pendientes del servidor. Cuando el valor es <= 1, las acciones de cancelación de preparación se ejecutan inmediatamente en la instrucción preparada CLOSE. Si se establece en > 1, estas llamadas se procesan por lotes para evitar la sobrecarga resultante de llamar a sp_unprepare con demasiada frecuencia.

  
## <a name="syntax"></a>Sintaxis  
  
```
public int getServerPreparedStatementDiscardThreshold();  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve el valor **int** de la propiedad de conexión **serverPreparedStatementDiscardThreshold**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Observaciones  
 Este método está disponible en la versión 6.4 y posteriores del controlador JDBC.
 
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

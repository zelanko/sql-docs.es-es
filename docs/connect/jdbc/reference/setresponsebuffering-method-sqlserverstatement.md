---
title: Método setResponseBuffering (SQLServerStatement) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apilocation:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: 9f489835-6cda-4c8c-b139-079639a169cf
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5abd900d5ba91939eb055b732a4710c4b89f0822
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="setresponsebuffering-method-sqlserverstatement"></a>Método setResponseBuffering (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece la respuesta de modo de almacenamiento en búfer para esta [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto entre mayúsculas y minúsculas **cadena completa** o **adaptable**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setResponseBuffering(java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *value*  
  
 A **cadena** que contiene el modo de almacenamiento en búfer de respuesta. El modo válido puede ser una de las siguientes cadenas entre mayúsculas y minúsculas: **completa** o **adaptable**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 **adaptable** especifica el almacenamiento en búfer los datos mínimos posibles cuando sea necesario.  
  
 **completa** especifica leer el resultado completo desde el servidor en tiempo de ejecución.  
  
 ADAPTATIVE es el valor predeterminado en la versión 2.0 y 3.0 del controlador JDBC. Full era el valor predeterminado antes de la versión 2.0 del controlador JDBC.  
  
 El [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método le permite invalidar la **responseBuffering** conexión **cadena** propiedad actuales [ SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto. Para obtener más información acerca de cómo utilizar el modo de almacenamiento en búfer de respuesta, consulte [usar almacenamiento en búfer adaptable](../../../connect/jdbc/using-adaptive-buffering.md).  
  
 Si la aplicación especifica un valor de parámetro no válido para la [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método, un [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) se produce.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)   
 [Usar el almacenamiento en búfer adaptable](../../../connect/jdbc/using-adaptive-buffering.md)  
  
  

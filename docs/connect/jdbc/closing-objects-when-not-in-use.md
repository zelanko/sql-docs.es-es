---
title: Cerrar los objetos no están siendo utilizados | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ce8f9b35-c761-4b0c-9a46-985eef2c2e0b
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 644f3f22d544940e1f0f72cdfbfd5351fee6f519
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32826700"
---
# <a name="closing-objects-when-not-in-use"></a>Cerrar los objetos cuando no se usan
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Cuando se trabaja con objetos de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], especialmente [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) o uno de la instrucción objetos como [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement ](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), debe cerrarlos explícitamente usando sus métodos cerrar cuando ya no son necesarios. Esto mejora el rendimiento al liberar lo antes posible los recursos del servidor y el controlador, en lugar de esperar a que el recolector de elementos no utilizados de la máquina virtual Java lo haga en su lugar.  
  
 Cerrar los objetos es especialmente importante para mantener una buena simultaneidad en el servidor cuando se usan bloqueos de desplazamiento. Los bloqueos de desplazamiento del búfer de captura al que se tuvo acceso por última vez se mantienen hasta que se cierra el conjunto de resultados. De igual forma, los identificadores que configuraron las instrucciones se conservan hasta que éstas se cierran. Si está reutilizando una conexión para varias instrucciones y las cierra antes de permitirles salir del ámbito, el servidor podrá limpiar los identificadores preparados con anterioridad.  
  
## <a name="see-also"></a>Vea también  
 [Mejorar el rendimiento y la confiabilidad con el controlador JDBC](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  

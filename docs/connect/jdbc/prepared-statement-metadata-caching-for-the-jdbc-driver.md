---
title: Preparado para el controlador JDBC el almacenamiento en caché de metadatos de instrucción | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a291cfb9497cee4fea87db915ca088069c1ec3cf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32833160"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>Almacenamiento en caché para el controlador JDBC de metadatos de instrucción preparada
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

En este artículo se proporciona información sobre los dos cambios que se implementan para mejorar el rendimiento del controlador.

## <a name="batching-of-unprepare-for-prepared-statements"></a>Procesamiento por lotes de cancelación de preparación para instrucciones preparadas
Puesto que se implementa la versión 6.1.6-preview, una mejora del rendimiento mediante la reducción del servidor de ida y vuelta a SQL Server. Anteriormente, para cada consulta prepareStatement, también se envía una llamada de cancelación de preparación. Ahora, el controlador es el procesamiento por lotes unprepare consultas hasta el umbral "ServerPreparedStatementDiscardThreshold", que tiene un valor predeterminado de 10.

> [!NOTE]  
>  Los usuarios pueden cambiar el valor predeterminado con el siguiente método: setServerPreparedStatementDiscardThreshold (el valor int)

Un cambio más introducido de 6.1.6-preview es que, antes de esto, controlador siempre llamaría sp_prepexec. Ahora, para la primera ejecución de una instrucción preparada, controlador llama a sp_executesql y para el resto se ejecuta sp_prepexec y le asigna un identificador. Pueden encontrar más detalles [aquí](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching).

> [!NOTE]  
>  Los usuarios pueden cambiar el comportamiento predeterminado para las versiones anteriores de siempre establecer enablePrepareOnFirstPreparedStatementCall para llamar a sp_prepexec **true** usando el método siguiente: setEnablePrepareOnFirstPreparedStatementCall (valor booleano)

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>Lista de las nuevas API introducidas con este cambio, para el procesamiento por lotes de cancelación de preparación para instrucciones preparadas

 **SQLServerConnection**
 
|Nuevo método|Description|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|Devuelve el número de pendientes actualmente preparada acciones de cancelación de preparación de instrucción.|
|void closeUnreferencedPreparedStatementHandles()|Fuerza a las solicitudes de unprepare para cualquier instrucción preparada descartados pendientes que se ejecute.|
|booleano getEnablePrepareOnFirstPreparedStatementCall()|Devuelve el comportamiento de una instancia de conexión específica. Si es false la primera ejecución y llama a sp_executesql no prepara una instrucción, una vez que la segunda ejecución ocurre llama sp_prepexec y un identificador de instrucción preparada realmente de la instalación. Después de las ejecuciones llamadas sp_execute. Esto evita la necesidad de sp_unprepare en la instrucción preparada cierre si la instrucción solo se ejecuta una vez. El valor predeterminado de esta opción se puede cambiar por setDefaultEnablePrepareOnFirstPreparedStatementCall() que realiza la llamada.|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|Especifica el comportamiento de una instancia de conexión específica. Si el valor es false la primera ejecución y llama a sp_executesql no prepara una instrucción, una vez que la segunda ejecución ocurre llama sp_prepexec y un identificador de instrucción preparada realmente de la instalación. Después de las ejecuciones llamadas sp_execute. Esto evita la necesidad de sp_unprepare en la instrucción preparada cierre si la instrucción solo se ejecuta una vez.|
|int getServerPreparedStatementDiscardThreshold()|Devuelve el comportamiento de una instancia de conexión específica. Esta configuración controla cuántas pendientes preparado descarte instrucción acciones (sp_unprepare) pueden estar pendientes por conexión antes de que se ejecuta una llamada para limpiar los controladores pendientes en el servidor. Si el valor es < = 1, cancelación de preparación de las acciones se ejecutan inmediatamente en cierre la instrucción preparada. Si se establece en {@literal >} 1, estas llamadas se procesan por lotes juntos para evitar una sobrecarga de sp_unprepare que realiza la llamada con demasiada frecuencia. El valor predeterminado de esta opción se puede cambiar por getDefaultServerPreparedStatementDiscardThreshold() que realiza la llamada.|
|void setServerPreparedStatementDiscardThreshold(int value)|Especifica el comportamiento de una instancia de conexión específica. Esta configuración controla cuántas pendientes preparado descarte instrucción acciones (sp_unprepare) pueden estar pendientes por conexión antes de que se ejecuta una llamada para limpiar los controladores pendientes en el servidor. Si el valor es < = 1 unprepare acciones se ejecutan inmediatamente en cierre la instrucción preparada. Si se establece en 1 > estas llamadas se procesan por lotes juntos para evitar una sobrecarga de la llamada a sp_unprepare con demasiada frecuencia.|

 **SQLServerDataSource**
 
|Nuevo método|Description|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|Si esta configuración es false la primera ejecución de una instrucción preparada y llama a sp_executesql no prepara una instrucción, una vez que la segunda ejecución ocurre llama sp_prepexec y un identificador de instrucción preparada realmente de la instalación. Después de las ejecuciones llamadas sp_execute. Esto evita la necesidad de sp_unprepare en la instrucción preparada cierre si la instrucción solo se ejecuta una vez.|
|booleano getEnablePrepareOnFirstPreparedStatementCall()|Si esta configuración se devuelve false la primera ejecución de una instrucción preparada llama a sp_executesql y no prepara una instrucción, una vez que se produce la segunda ejecución, llama a sp_prepexec y un identificador de instrucción preparada realmente de la instalación. Después de las ejecuciones llamadas sp_execute. Esto evita la necesidad de sp_unprepare en la instrucción preparada cierre si la instrucción solo se ejecuta una vez.|
|void setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|Esta configuración controla cuántas pendientes preparado descarte instrucción acciones (sp_unprepare) pueden estar pendientes por conexión antes de que se ejecuta una llamada para limpiar los controladores pendientes en el servidor. Si el valor es < = 1 unprepare acciones se ejecutan inmediatamente en cierre la instrucción preparada. Si se establece en {@literal >} 1 estas llamadas se procesan por lotes juntos para evitar una sobrecarga de la llamada a sp_unprepare con demasiada frecuencia|
|int getServerPreparedStatementDiscardThreshold()|Esta configuración controla cuántas pendientes preparado descarte instrucción acciones (sp_unprepare) pueden estar pendientes por conexión antes de que se ejecuta una llamada para limpiar los controladores pendientes en el servidor. Si el valor es < = 1 unprepare acciones se ejecutan inmediatamente en cierre la instrucción preparada. Si se establece en {@literal >} 1 estas llamadas se procesan por lotes juntos para evitar una sobrecarga de la llamada a sp_unprepare con demasiada frecuencia.|

## <a name="prepared-statement-metatada-caching"></a>Almacenamiento en caché de metadatos de la instrucción preparada
A partir de la versión de 6.3.0-preview, Microsoft JDBC driver para SQL Server admite la caché de la instrucción preparada. Antes de la vista previa de v6.3.0, si uno ejecuta una consulta que ya está preparada y almacenan en la memoria caché, volver a llamar a la misma consulta no darán como resultado de preparación. Ahora, el controlador busca la consulta en caché y buscar el identificador y ejecutarlo con sp_execute.
Almacenamiento en caché de metadatos de instrucción preparada es **deshabilitado** de forma predeterminada. Para habilitarlo, debe llamar al método en el objeto de conexión:

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

Por ejemplo: `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>Lista de las nuevas API introducidas con este cambio, para la instrucción preparada almacenamiento en caché de metadatos

 **SQLServerConnection**
 
|Nuevo método|Description|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean value)|Establece la agrupación de instrucciones en true o false.|
|booleano getDisableStatementPooling()|Devuelve true si la agrupación de instrucción está deshabilitada.|
|void setStatementPoolingCacheSize(int value)|Especifica el tamaño de la caché de instrucciones preparadas para esta conexión. Un valor menor que 1 no significa caché.|
|int getStatementPoolingCacheSize()|Devuelve el tamaño de la caché de instrucciones preparadas para esta conexión. Un valor menor que 1 no significa caché.|
|int getStatementHandleCacheEntryCount()|Devuelve el número actual de identificadores de instrucciones preparadas agrupados.|
|booleano isPreparedStatementCachingEnabled()|Si la agrupación de instrucción está habilitada o no para esta conexión.|

 **SQLServerDataSource**
 
|Nuevo método|Description|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean disableStatementPooling)|Establece la instrucción de agrupación en true o false|
|booleano getDisableStatementPooling()|Devuelve true si la agrupación de instrucción está deshabilitada.|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|Especifica el tamaño de la caché de instrucciones preparadas para esta conexión. Un valor menor que 1 no significa caché.|
|int getStatementPoolingCacheSize()|Devuelve el tamaño de la caché de instrucciones preparadas para esta conexión. Un valor menor que 1 no significa caché.|

## <a name="see-also"></a>Vea también  
 [Mejorar el rendimiento y la confiabilidad con el controlador JDBC](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  

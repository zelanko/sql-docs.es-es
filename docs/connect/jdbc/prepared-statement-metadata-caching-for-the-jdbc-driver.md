---
title: Almacenamiento en caché de metadatos de instrucciones preparadas para el controlador JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97224f53bb716abe3b79dd00df12d0eed4a63cec
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027838"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>Almacenamiento en caché de metadatos de instrucciones preparadas para el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

En este artículo se proporciona información sobre los dos cambios que se implementan para mejorar el rendimiento del controlador.

## <a name="batching-of-unprepare-for-prepared-statements"></a>Procesamiento por lotes de la despreparación para las instrucciones preparadas
Desde la versión 6.1.6-Preview, se implementó una mejora en el rendimiento mediante la reducción de los recorridos de ida y vuelta del servidor a SQL Server. Anteriormente, para cada consulta de prepareStatement, también se enviaba una llamada a Unprepare. Ahora, el controlador procesa por lotes las consultas de despreparación hasta el umbral "ServerPreparedStatementDiscardThreshold", que tiene un valor predeterminado de 10.

> [!NOTE]  
>  Los usuarios pueden cambiar el valor predeterminado con el siguiente método: setServerPreparedStatementDiscardThreshold (valor int)

Uno de los cambios más introducidos en 6.1.6-Preview es que, antes de esto, el controlador siempre llamaría a sp_prepexec. Ahora, para la primera ejecución de una instrucción preparada, el controlador llama a sp_executesql y para el resto ejecuta sp_prepexec y le asigna un identificador. Puede encontrar más detalles [aquí](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching).

> [!NOTE]  
>  Los usuarios pueden cambiar el comportamiento predeterminado a las versiones anteriores de llamando siempre a sp_prepexec estableciendo enablePrepareOnFirstPreparedStatementCall en **true** usando el método siguiente: setEnablePrepareOnFirstPreparedStatementCall (valor booleano )

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>Lista de las nuevas API introducidas con este cambio, para el procesamiento por lotes de la despreparación para las instrucciones preparadas

 **SQLServerConnection**
 
|Nuevo método|Descripción|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|Devuelve el número de acciones de despreparación de la instrucción preparada actualmente pendiente.|
|void closeUnreferencedPreparedStatementHandles()|Fuerza la ejecución de las solicitudes de desactivación de las instrucciones preparadas descartadas pendientes.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|Devuelve el comportamiento de una instancia de conexión concreta. Si es false, la primera ejecución llama a sp_executesql y no prepara una instrucción, una vez que se produce la segunda ejecución, llama a sp_prepexec y, en realidad, configura un identificador de instrucción preparado. Las siguientes ejecuciones llama a sp_execute. Esto libera la necesidad de sp_unprepare en el cierre de la instrucción preparada si la instrucción solo se ejecuta una vez. El valor predeterminado de esta opción se puede cambiar mediante una llamada a setDefaultEnablePrepareOnFirstPreparedStatementCall ().|
|void setEnablePrepareOnFirstPreparedStatementCall (valor booleano)|Especifica el comportamiento de una instancia de conexión concreta. Si el valor es false, la primera ejecución llama a sp_executesql y no prepara una instrucción, una vez que se produce la segunda ejecución, llama a sp_prepexec y, en realidad, configura un identificador de instrucción preparado. Las siguientes ejecuciones llama a sp_execute. Esto libera la necesidad de sp_unprepare en el cierre de la instrucción preparada si la instrucción solo se ejecuta una vez.|
|int getServerPreparedStatementDiscardThreshold()|Devuelve el comportamiento de una instancia de conexión concreta. Esta configuración controla el número de acciones de descarte de instrucciones preparada pendientes (sp_unprepare) que pueden quedar pendientes por conexión antes de que se ejecute una llamada para limpiar los controladores pendientes en el servidor. Si el valor es < = 1, las acciones de despreparar se ejecutan inmediatamente en el cierre de la instrucción preparada. Si se establece en {@literal >} 1, estas llamadas se agrupan por lotes para evitar la sobrecarga de llamar a sp_unprepare con demasiada frecuencia. El valor predeterminado de esta opción se puede cambiar mediante una llamada a getDefaultServerPreparedStatementDiscardThreshold ().|
|void setServerPreparedStatementDiscardThreshold (valor int)|Especifica el comportamiento de una instancia de conexión concreta. Esta configuración controla el número de acciones de descarte de instrucciones preparada pendientes (sp_unprepare) que pueden quedar pendientes por conexión antes de que se ejecute una llamada para limpiar los controladores pendientes en el servidor. Si el valor es < = 1 las acciones de despreparación se ejecutan inmediatamente en el cierre de la instrucción preparada. Si se establece en > 1, estas llamadas se agrupan por lotes para evitar la sobrecarga de llamar a sp_unprepare con demasiada frecuencia.|

 **SQLServerDataSource**
 
|Nuevo método|Descripción|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall (Boolean enablePrepareOnFirstPreparedStatementCall)|Si esta configuración es falsa, la primera ejecución de una instrucción preparada llama a sp_executesql y no prepara una instrucción, una vez que se produce la segunda ejecución, llama a sp_prepexec y, en realidad, configura un identificador de instrucción preparado. Las siguientes ejecuciones llama a sp_execute. Esto libera la necesidad de sp_unprepare en el cierre de la instrucción preparada si la instrucción solo se ejecuta una vez.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|Si esta configuración devuelve false, la primera ejecución de una instrucción preparada llama a sp_executesql y no prepara una instrucción, una vez que se produce la segunda ejecución, llama a sp_prepexec y, en realidad, configura un identificador de instrucción preparado. Las siguientes ejecuciones llama a sp_execute. Esto libera la necesidad de sp_unprepare en el cierre de la instrucción preparada si la instrucción solo se ejecuta una vez.|
|void setServerPreparedStatementDiscardThreshold (int serverPreparedStatementDiscardThreshold)|Esta configuración controla el número de acciones de descarte de instrucciones preparada pendientes (sp_unprepare) que pueden quedar pendientes por conexión antes de que se ejecute una llamada para limpiar los controladores pendientes en el servidor. Si el valor es < = 1 las acciones de despreparación se ejecutan inmediatamente en el cierre de la instrucción preparada. Si se establece en {@literal >} 1, estas llamadas se agrupan por lotes para evitar la sobrecarga de llamar a sp_unprepare con demasiada frecuencia.|
|int getServerPreparedStatementDiscardThreshold()|Esta configuración controla el número de acciones de descarte de instrucciones preparada pendientes (sp_unprepare) que pueden quedar pendientes por conexión antes de que se ejecute una llamada para limpiar los controladores pendientes en el servidor. Si el valor es < = 1 las acciones de despreparación se ejecutan inmediatamente en el cierre de la instrucción preparada. Si se establece en {@literal >} 1, estas llamadas se agrupan por lotes para evitar la sobrecarga de llamar a sp_unprepare con demasiada frecuencia.|

## <a name="prepared-statement-metatada-caching"></a>Instrucción preparada metadatos Caching
A partir de la versión de 6.3.0-Preview, Microsoft JDBC driver for SQL Server admite el almacenamiento en caché de instrucciones preparado. Antes de v 6.3.0-Preview, si una ejecuta una consulta que ya se ha preparado y almacenado en la memoria caché, la llamada a la misma consulta no dará como resultado la preparación. Ahora, el controlador busca la consulta en la memoria caché y busca el identificador y lo ejecuta con sp_execute.
Instrucción preparada el almacenamiento en  **caché** de metadatos está deshabilitado de forma predeterminada. Para habilitarlo, debe llamar al método siguiente en el objeto de conexión:

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

Por ejemplo: `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>Lista de las nuevas API introducidas con este cambio, para el almacenamiento en caché de metadatos de instrucciones preparadas

 **SQLServerConnection**
 
|Nuevo método|Descripción|  
|-----------|-----------------|  
|void setDisableStatementPooling (valor booleano)|Establece la agrupación de instrucciones en true o false.|
|boolean getDisableStatementPooling()|Devuelve true si la agrupación de instrucciones está deshabilitada.|
|void setStatementPoolingCacheSize(int value)|Especifica el tamaño de la memoria caché de instrucciones preparada para esta conexión. Un valor menor que 1 significa que no hay caché.|
|int getStatementPoolingCacheSize()|Devuelve el tamaño de la memoria caché de instrucciones preparada para esta conexión. Un valor menor que 1 significa que no hay caché.|
|int getStatementHandleCacheEntryCount()|Devuelve el número actual de identificadores de instrucción preparados agrupados.|
|Boolean isPreparedStatementCachingEnabled ()|Indica si la agrupación de instrucciones está habilitada o no para esta conexión.|

 **SQLServerDataSource**
 
|Nuevo método|Descripción|  
|-----------|-----------------|  
|void setDisableStatementPooling (Boolean disableStatementPooling)|Establece la agrupación de instrucciones en true o false.|
|boolean getDisableStatementPooling()|Devuelve true si la agrupación de instrucciones está deshabilitada.|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|Especifica el tamaño de la memoria caché de instrucciones preparada para esta conexión. Un valor menor que 1 significa que no hay caché.|
|int getStatementPoolingCacheSize()|Devuelve el tamaño de la memoria caché de instrucciones preparada para esta conexión. Un valor menor que 1 significa que no hay caché.|

## <a name="see-also"></a>Vea también  
 [Mejora del rendimiento y la confiabilidad con el controlador JDBC](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  

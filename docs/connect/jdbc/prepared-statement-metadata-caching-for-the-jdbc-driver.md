---
title: Almacenamiento en caché de metadatos de instrucción preparado para el controlador JDBC | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 58ebcb2560e3b03703d7a419b28c6c04e41c19f1
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794088"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>Almacenamiento en caché de metadatos de instrucción preparado para el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

En este artículo se proporciona información sobre los dos cambios que se implementan para mejorar el rendimiento del controlador.

## <a name="batching-of-unprepare-for-prepared-statements"></a>Cancelaciones de procesamiento por lotes de preparación para instrucciones preparadas
Puesto que se implementó la versión 6.1.6-preview, una mejora del rendimiento mediante la reducción del servidor de ida y vuelta a SQL Server. Anteriormente, para cada consulta prepareStatement, también se ha enviado una llamada a unprepare. Ahora, el controlador es el procesamiento por lotes unprepare consultas hasta que el umbral de "Valor de ServerPreparedStatementDiscardThreshold", que tiene un valor predeterminado de 10.

> [!NOTE]  
>  Los usuarios pueden cambiar el valor predeterminado con el siguiente método: setServerPreparedStatementDiscardThreshold (valor int)

Un cambio más introducido desde 6.1.6-preview es que, antes de esto, controlador siempre llamaría sp_prepexec. Ahora, para la primera ejecución de una instrucción preparada, controlador llama a sp_executesql y el resto ejecuta sp_prepexec y le asigna un identificador. Pueden encontrar más detalles [aquí](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching).

> [!NOTE]  
>  Los usuarios pueden cambiar el comportamiento predeterminado para las versiones anteriores de siempre enablePrepareOnFirstPreparedStatementCall establecer para llamar a sp_prepexec **true** utilizando el método siguiente: setEnablePrepareOnFirstPreparedStatementCall (valor booleano)

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>Lista de las nuevas API incluidas con este cambio, para el procesamiento por lotes de cancelaciones de preparación para instrucciones preparadas

 **SQLServerConnection**
 
|Nuevo método|Descripción|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|Devuelve el número de pendientes actualmente preparada instrucción unprepare acciones.|
|void closeUnreferencedPreparedStatementHandles()|Obliga a las solicitudes de unprepare para cualquier instrucción preparada descartados pendientes que se ejecutará.|
|booleano getEnablePrepareOnFirstPreparedStatementCall()|Devuelve el comportamiento de una instancia de la conexión específica. Si es false la primera ejecución y llama a sp_executesql no prepara una instrucción, una vez que se produce la segunda ejecución llama a sp_prepexec y configurar realmente un identificador de instrucción preparada. Sp_execute de llamadas de las ejecuciones siguientes. Cerrar Esto evita la necesidad de sp_unprepare en la instrucción preparada si la instrucción solo se ejecuta una vez. El valor predeterminado para esta opción se puede cambiar por setDefaultEnablePrepareOnFirstPreparedStatementCall() que realiza la llamada.|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|Especifica el comportamiento de una instancia de la conexión específica. Si el valor es false la primera ejecución y llama a sp_executesql no prepara una instrucción, una vez que se produce la segunda ejecución llama a sp_prepexec y configurar realmente un identificador de instrucción preparada. Sp_execute de llamadas de las ejecuciones siguientes. Cerrar Esto evita la necesidad de sp_unprepare en la instrucción preparada si la instrucción solo se ejecuta una vez.|
|int getServerPreparedStatementDiscardThreshold()|Devuelve el comportamiento de una instancia de la conexión específica. Esta configuración controla cuántos pendientes preparado descarte instrucción acciones (sp_unprepare) pueden estar pendientes por conexión antes de que se ejecuta una llamada para limpiar los controladores pendientes en el servidor. Si el valor es < = 1, unprepare acciones se ejecutan inmediatamente en la instrucción preparada cierre. Si se establece en {@literal >} 1, estas llamadas se procesan por lotes juntos para evitar una sobrecarga de llamada sp_unprepare con demasiada frecuencia. El valor predeterminado para esta opción se puede cambiar por getDefaultServerPreparedStatementDiscardThreshold() que realiza la llamada.|
|void setServerPreparedStatementDiscardThreshold(int value)|Especifica el comportamiento de una instancia de la conexión específica. Esta configuración controla cuántos pendientes preparado descarte instrucción acciones (sp_unprepare) pueden estar pendientes por conexión antes de que se ejecuta una llamada para limpiar los controladores pendientes en el servidor. Si el valor es < = 1 unprepare acciones se ejecutan inmediatamente en la instrucción preparada cierre. Si se establece en 1 > estas llamadas se procesan por lotes juntos para evitar una sobrecarga de la llamada a sp_unprepare con demasiada frecuencia.|

 **SQLServerDataSource**
 
|Nuevo método|Descripción|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|Si esta configuración es false la primera ejecución de una instrucción preparada y llama a sp_executesql no prepara una instrucción, una vez que se produce la segunda ejecución llama a sp_prepexec y configurar realmente un identificador de instrucción preparada. Sp_execute de llamadas de las ejecuciones siguientes. Cerrar Esto evita la necesidad de sp_unprepare en la instrucción preparada si la instrucción solo se ejecuta una vez.|
|booleano getEnablePrepareOnFirstPreparedStatementCall()|Si esta configuración se devuelve false, la primera ejecución de una instrucción preparada llama a sp_executesql y no prepara una instrucción, una vez que se produce la segunda ejecución, llama a sp_prepexec y configurar realmente un identificador de instrucción preparada. Sp_execute de llamadas de las ejecuciones siguientes. Cerrar Esto evita la necesidad de sp_unprepare en la instrucción preparada si la instrucción solo se ejecuta una vez.|
|void setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|Esta configuración controla cuántos pendientes preparado descarte instrucción acciones (sp_unprepare) pueden estar pendientes por conexión antes de que se ejecuta una llamada para limpiar los controladores pendientes en el servidor. Si el valor es < = 1 unprepare acciones se ejecutan inmediatamente en la instrucción preparada cierre. Si se establece en {@literal >} 1 estas llamadas se procesan por lotes juntos para evitar una sobrecarga de la llamada a sp_unprepare con demasiada frecuencia|
|int getServerPreparedStatementDiscardThreshold()|Esta configuración controla cuántos pendientes preparado descarte instrucción acciones (sp_unprepare) pueden estar pendientes por conexión antes de que se ejecuta una llamada para limpiar los controladores pendientes en el servidor. Si el valor es < = 1 unprepare acciones se ejecutan inmediatamente en la instrucción preparada cierre. Si se establece en {@literal >} 1 estas llamadas se procesan por lotes juntos para evitar una sobrecarga de la llamada a sp_unprepare con demasiada frecuencia.|

## <a name="prepared-statement-metatada-caching"></a>Almacenamiento en caché de metadatos de instrucción preparada
A partir de la versión 6.3.0-preview, Microsoft JDBC driver para SQL Server admite el almacenamiento en caché de la instrucción preparada. Antes de v6.3.0-preview, si uno ejecuta una consulta que se haya preparado y almacenan en la memoria caché, ya volver a llamar a la misma consulta no dará como resultado de preparación. Ahora, el controlador busca la consulta en caché y buscar el identificador y ejecutarlo con sp_execute.
Almacenamiento en caché de metadatos de instrucción preparada es **deshabilitado** de forma predeterminada. Para habilitarlos, debe llamar al método siguiente en el objeto de conexión:

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

Por ejemplo: `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>Lista de las nuevas API incluidas con este cambio, para la instrucción preparada almacenamiento en caché de metadatos

 **SQLServerConnection**
 
|Nuevo método|Descripción|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean value)|Establece la agrupación de instrucciones en true o false.|
|boolean getDisableStatementPooling()|Devuelve true si se deshabilita la agrupación de instrucciones.|
|void setStatementPoolingCacheSize(int value)|Especifica el tamaño de la caché de la instrucción preparada para esta conexión. Un valor menor que 1 no significa memoria caché.|
|int getStatementPoolingCacheSize()|Devuelve el tamaño de la caché de la instrucción preparada para esta conexión. Un valor menor que 1 no significa memoria caché.|
|int getStatementHandleCacheEntryCount()|Devuelve el número actual de identificadores de instrucción preparada agrupados.|
|booleano isPreparedStatementCachingEnabled()|Si está habilitada la agrupación de instrucciones o no para esta conexión.|

 **SQLServerDataSource**
 
|Nuevo método|Descripción|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean disableStatementPooling)|Establece la instrucción de agrupación en true o false|
|boolean getDisableStatementPooling()|Devuelve true si se deshabilita la agrupación de instrucciones.|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|Especifica el tamaño de la caché de la instrucción preparada para esta conexión. Un valor menor que 1 no significa memoria caché.|
|int getStatementPoolingCacheSize()|Devuelve el tamaño de la caché de la instrucción preparada para esta conexión. Un valor menor que 1 no significa memoria caché.|

## <a name="see-also"></a>Consulte también  
 [Mejorar el rendimiento y la confiabilidad con el controlador JDBC](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  

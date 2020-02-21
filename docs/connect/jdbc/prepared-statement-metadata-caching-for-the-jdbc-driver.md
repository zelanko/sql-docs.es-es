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
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027838"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>Almacenamiento en caché de metadatos de instrucciones preparadas para el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

En este artículo se proporciona información sobre los dos cambios que se implementan para mejorar el rendimiento del controlador.

## <a name="batching-of-unprepare-for-prepared-statements"></a>Procesamiento por lotes de la cancelación de preparación para instrucciones preparadas
Desde la versión preliminar 6.1.6, se implementó una mejora en el rendimiento a través de la reducción de los ciclos de ida y vuelta del servidor en SQL Server. Anteriormente, para todas las consultas prepareStatement, también se envió una llamada a la cancelación de preparación. Ahora, el controlador procesa por lotes consultas de cancelación de preparación hasta el umbral "ServerPreparedStatementDiscardThreshold", que tiene un valor predeterminado de 10.

> [!NOTE]  
>  Los usuarios pueden cambiar el valor predeterminado con el siguiente método: setServerPreparedStatementDiscardThreshold(int value)

Un cambio más presentado en la versión preliminar 6.1.6 es que, antes de esta, el controlador siempre llamaría a sp_prepexec. Ahora, para la primera ejecución de una instrucción preparada, el controlador llama a sp_executesql y para el resto ejecuta sp_prepexec y le asigna un identificador. Se pueden encontrar más detalles [aquí](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching).

> [!NOTE]  
>  Los usuarios pueden cambiar el comportamiento predeterminado a las versiones anteriores de las llamadas en todo momento a sp_prepexec estableciendo enablePrepareOnFirstPreparedStatementCall en **true** mediante el siguiente método: setEnablePrepareOnFirstPreparedStatementCall(boolean value)

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>Lista de las nuevas API presentadas con este cambio, para el procesamiento por lotes de la cancelación de preparación para instrucciones preparadas

 **SQLServerConnection**
 
|Nuevo método|Descripción|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|Devuelve el número de acciones de cancelación de preparación de instrucciones preparadas pendientes.|
|void closeUnreferencedPreparedStatementHandles()|Fuerza las solicitudes de cancelación de preparación para cualquier instrucción preparada descartada pendiente que se vaya a ejecutar.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|Devuelve el comportamiento de una instancia de conexión específica. Si es false, la primera ejecución llama a sp_executesql y no prepara una instrucción. Una vez que se produce la segunda ejecución, llama a sp_prepexec y configura realmente un identificador de instrucción preparada. Las siguientes ejecuciones llaman a sp_execute. Esto alivia la necesidad de sp_unprepare al cerrar la instrucción preparada si la instrucción solo se ejecuta una vez. El valor predeterminado de esta opción se puede cambiar llamando a setDefaultEnablePrepareOnFirstPreparedStatementCall().|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|Especifica el comportamiento de una instancia de conexión específica. Si el valor es false, la primera ejecución llama a sp_executesql y no prepara una instrucción. Una vez que se produce la segunda ejecución, llama a sp_prepexec y configura realmente un identificador de instrucción preparada. Las siguientes ejecuciones llaman a sp_execute. Esto alivia la necesidad de sp_unprepare en la instrucción preparada CLOSE si la instrucción solo se ejecuta una vez.|
|int getServerPreparedStatementDiscardThreshold()|Devuelve el comportamiento de una instancia de conexión específica. Este valor controla cuántas acciones de descarte de instrucción preparada pendientes (sp_unprepare) pueden estar pendientes por conexión antes de que se ejecute una llamada para limpiar los identificadores pendientes del servidor. Si el valor es <= 1, las acciones de cancelación de preparación se ejecutan inmediatamente en la instrucción preparada CLOSE. Si se establece en {@literal >} 1, estas llamadas se procesan por lotes para evitar la sobrecarga resultante de llamar a sp_unprepare con demasiada frecuencia. El valor predeterminado de esta opción se puede cambiar llamando a getDefaultServerPreparedStatementDiscardThreshold().|
|void setServerPreparedStatementDiscardThreshold(int value)|Especifica el comportamiento de una instancia de conexión específica. Este valor controla cuántas acciones de descarte de instrucción preparada pendientes (sp_unprepare) pueden estar pendientes por conexión antes de que se ejecute una llamada para limpiar los identificadores pendientes del servidor. Si el valor es <= 1, las acciones de cancelación de preparación se ejecutan inmediatamente en la instrucción preparada CLOSE. Si se establece en > 1, estas llamadas se procesan por lotes para evitar la sobrecarga resultante de llamar a sp_unprepare con demasiada frecuencia.|

 **SQLServerDataSource**
 
|Nuevo método|Descripción|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|Si esta configuración es false, la primera ejecución de una instrucción preparada llama a sp_executesql y no prepara una instrucción. Una vez que se produce la segunda ejecución, llama a sp_prepexec y configura realmente un identificador de instrucción preparada. Las siguientes ejecuciones llaman a sp_execute. Esto alivia la necesidad de sp_unprepare en la instrucción preparada CLOSE si la instrucción solo se ejecuta una vez.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|Si esta configuración devuelve false, la primera ejecución de una instrucción preparada llama a sp_executesql y no prepara una instrucción. Una vez que se produce la segunda ejecución, llama a sp_prepexec y configura realmente un identificador de instrucción preparada. Las siguientes ejecuciones llaman a sp_execute. Esto alivia la necesidad de sp_unprepare en la instrucción preparada CLOSE si la instrucción solo se ejecuta una vez.|
|void setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|Este valor controla cuántas acciones de descarte de instrucción preparada pendientes (sp_unprepare) pueden estar pendientes por conexión antes de que se ejecute una llamada para limpiar los identificadores pendientes del servidor. Si el valor es <= 1, las acciones de cancelación de preparación se ejecutan inmediatamente en la instrucción preparada CLOSE. Si se establece en {@literal >} 1, estas llamadas se procesan por lotes para evitar la sobrecarga resultante de llamar a sp_unprepare con demasiada frecuencia.|
|int getServerPreparedStatementDiscardThreshold()|Este valor controla cuántas acciones de descarte de instrucción preparada pendientes (sp_unprepare) pueden estar pendientes por conexión antes de que se ejecute una llamada para limpiar los identificadores pendientes del servidor. Si el valor es <= 1, las acciones de cancelación de preparación se ejecutan inmediatamente en la instrucción preparada CLOSE. Si se establece en {@literal >} 1, estas llamadas se procesan por lotes para evitar la sobrecarga resultante de llamar a sp_unprepare con demasiada frecuencia.|

## <a name="prepared-statement-metatada-caching"></a>Almacenamiento en caché de metadatos de instrucción preparada
A partir de la versión preliminar 6.3.0, Microsoft JDBC Driver para SQL Server admite el almacenamiento en caché de instrucciones preparadas. Antes de la versión preliminar 6.3.0, si se ejecutaba una consulta que ya se había preparado y almacenado en la caché, llamar de nuevo a la misma consulta no conllevará su preparación. Ahora, el controlador busca la consulta en la caché y busca el identificador y lo ejecuta con sp_execute.
Instrucción preparada el almacenamiento en  **caché** de metadatos está deshabilitado de forma predeterminada. Para su habilitación, debe llamar al siguiente método en el objeto de conexión:

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

Por ejemplo: `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>Lista de las nuevas API presentadas con este cambio, para el almacenamiento en caché de metadatos de instrucción preparada

 **SQLServerConnection**
 
|Nuevo método|Descripción|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean value)|Establece la agrupación de instrucciones en true o false.|
|boolean getDisableStatementPooling()|Devuelve true si la agrupación de instrucciones está deshabilitada.|
|void setStatementPoolingCacheSize(int value)|Especifica el tamaño de la caché de instrucciones preparadas para esta conexión. Un valor inferior a 1 significa sin caché.|
|int getStatementPoolingCacheSize()|Devuelve el tamaño de la caché de instrucciones preparadas para esta conexión. Un valor inferior a 1 significa sin caché.|
|int getStatementHandleCacheEntryCount()|Devuelve el número actual de identificadores de instrucción preparada agrupados.|
|boolean isPreparedStatementCachingEnabled()|Especifica si la agrupación de instrucciones está habilitada o no para esta conexión.|

 **SQLServerDataSource**
 
|Nuevo método|Descripción|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean disableStatementPooling)|Establece la agrupación de instrucciones en true o false.|
|boolean getDisableStatementPooling()|Devuelve true si la agrupación de instrucciones está deshabilitada.|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|Especifica el tamaño de la caché de instrucciones preparadas para esta conexión. Un valor inferior a 1 significa sin caché.|
|int getStatementPoolingCacheSize()|Devuelve el tamaño de la caché de instrucciones preparadas para esta conexión. Un valor inferior a 1 significa sin caché.|

## <a name="see-also"></a>Consulte también  
 [Mejora del rendimiento y la confiabilidad con el controlador JDBC](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  

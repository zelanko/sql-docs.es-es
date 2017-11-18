---
title: "Usar almacenamiento en búfer adaptable | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 92d4e3be-c3e9-4732-9a60-b57f4d0f7cb7
caps.latest.revision: 53
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 80944d5ebb5ec8c9f6ba98d9c520b10a0c4ade30
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="using-adaptive-buffering"></a>Usar el almacenamiento en búfer adaptable
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El almacenamiento en búfer adaptable está diseñado para recuperar cualquier tipo de datos de valores grandes sin sufrir la sobrecarga de los cursores de servidor. Las aplicaciones pueden utilizar la característica de almacenamiento en búfer adaptable con todas las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] que son compatibles con el controlador.  
  
 Normalmente, cuando la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ejecuta una consulta, lleva todos los resultados desde el servidor a la memoria de la aplicación. Aunque este enfoque reduce el consumo de recursos en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], puede producir un OutOfMemoryError en la aplicación JDBC para las consultas que producen resultados muy grandes.  
  
 Para permitir que las aplicaciones administren resultados muy grandes, el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona almacenamiento en búfer adaptable. Con almacenamiento en búfer adaptable, el controlador JDBC recupera los resultados de ejecución de la instrucción de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] como la aplicación los necesita, en lugar de todos a la vez. El controlador también descarta los resultados en cuanto la aplicación ya no puede tener acceso a ellos. Se incluyen a continuación algunos ejemplos en los que el almacenamiento en búfer adaptable puede ser útil:  
  
-   **La consulta genera un conjunto de resultados muy grande:** la aplicación puede ejecutar una instrucción SELECT que genera más filas de la aplicación puede almacenar en memoria. En versiones anteriores, la aplicación tenía que utilizar un cursor de servidor para evitar un OutOfMemoryError. El almacenamiento en búfer adaptable permite hacer un paso de solo lectura y solo avance de un conjunto de resultados arbitrariamente grande sin requerir un cursor de servidor.  
  
-   **La consulta genera gran**[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)**columnas o**[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)**los valores de parámetro:**  La aplicación puede recuperar un valor único (columna o parámetro OUT) que es demasiado grande para caber completamente en memoria de la aplicación.         Almacenamiento en búfer adaptable permite a la aplicación cliente recuperar este valor como una secuencia, utilizando el getAsciiStream, el getBinaryStream o los métodos de getCharacterStream. La aplicación recupera el valor de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tal y como lee de la secuencia.  
  
> [!NOTE]  
>  Con el almacenamiento en búfer adaptable, el controlador JDBC solamente almacena en búfer las cantidad de datos que debe almacenar. El controlador no proporciona un método público para controlar o limitar el tamaño del búfer.  
  
## <a name="setting-adaptive-buffering"></a>Establecer el almacenamiento en búfer adaptable  
 A partir de la versión 2.0, el comportamiento predeterminado del controlador del controlador JDBC es "**adaptable**". Dicho de otro modo, para obtener el comportamiento de almacenamiento en búfer adaptable, su aplicación no tiene que solicitar explícitamente el comportamiento adaptable. En la versión 1.2, sin embargo, el modo de almacenamiento en búfer era "**completa**" de forma predeterminada y la aplicación tenía que solicitar el modo de almacenamiento en búfer adaptable explícitamente.  
  
 Hay tres formas en las que una aplicación puede solicitar que la ejecución de una instrucción deba usar el almacenamiento en búfer adaptable:  
  
-   La aplicación puede establecer la propiedad de conexión **responseBuffering** en "ADAPTATIVE". Para obtener más información acerca de cómo establecer las propiedades de conexión, vea [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
-   La aplicación puede utilizar el [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md) método de la [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto que se va a establecer el modo de todas las conexiones creadas a través de la que el almacenamiento en búfer de respuesta [ SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto.  
  
-   La aplicación puede utilizar el [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método de la [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) clase para establecer el modo de un objeto de instrucción concreto del búfer de respuestas.  
  
 Cuando se utiliza la versión 1.2, debe convertir el objeto de instrucción para las aplicaciones del controlador JDBC una [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) clase se debe utilizar el [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método. Los ejemplos de código en el [muestra de datos grandes de lectura](../../connect/jdbc/reading-large-data-sample.md) y [leer datos de gran tamaño con un ejemplo de procedimientos almacenados](../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md) muestran el uso antiguo.  
  
 Sin embargo, con la versión 2.0 del controlador JDBC, las aplicaciones pueden usar el [isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) método y [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) método para tener acceso a la funcionalidad específica del proveedor sin ninguna suposición sobre el jerarquía de clases de implementación. Por ejemplo de código, vea la [muestra de datos grandes actualización](../../connect/jdbc/updating-large-data-sample.md) tema.  
  
## <a name="retrieving-large-data-with-adaptive-buffering"></a>Recuperar datos grandes con el almacenamiento en búfer adaptable  
 Cuando se leen valores grandes una vez mediante el uso de get\<tipo > se obtiene acceso a métodos de secuencia y las columnas del conjunto de resultados y los parámetros OUT CallableStatement en el orden devuelto por la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], almacenamiento en búfer adaptable reduce la aplicación uso de memoria al procesar los resultados. Al utilizar el almacenamiento en búfer adaptable:  
  
-   Get\<tipo > transmitir métodos definidos en el [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) y [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) clases devuelven secuencias de una sola lectura de forma predeterminada, aunque se pueden restablecer las secuencias si marca la aplicación. Si la aplicación desea `reset` el flujo, tiene que llamar el `mark` método en el que transmitir en primer lugar.  
  
-   Get\<tipo > transmitir métodos definidos en el [SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md) y [SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md) clases devuelven secuencias que siempre se pueden mover la posición de inicio de la secuencia sin llamar a la `mark` método.  
  
 Cuando la aplicación utiliza el almacenamiento en búfer adaptable, los valores recuperados por get\<tipo > métodos flujos solo se pueden recuperar una vez. Si intenta llamar a cualquier get\<tipo > método en la misma columna o parámetro después de llamar a get\<tipo > se produce el método de secuencia del mismo objeto, una excepción con el mensaje, "los datos se ha tenido acceso y no están disponibles para el columna o parámetro".  
  
> [!NOTE]
> Una llamada a ResultSet.close() durante el procesamiento de un conjunto de resultados requeriría el controlador JDBC de Microsoft para SQL Server leer y descartar todos los paquetes restantes. Esto puede tardar mucho tiempo si la consulta devuelve un conjunto de datos grande y especialmente si la conexión de red es lenta.     
  
## <a name="guidelines-for-using-adaptive-buffering"></a>Directrices para el uso del almacenamiento en búfer adaptable  
 Los desarrolladores de software deberían seguir estas importantes directrices para disminuir la utilización de memoria por parte de la aplicación:  
  
-   Evite el uso de la propiedad de cadena de conexión **selectMethod = cursor** permitir que la aplicación procesar un gran resultado establecido. La característica de almacenamiento en búfer adaptable permite a las aplicaciones procesar los conjuntos de resultados de solo avance y solo lectura muy grandes sin utilizar un cursor de servidor. Tenga en cuenta que al establecer **selectMethod = cursor**todo solo avance, conjuntos de resultados de solo lectura producidos por esa conexión se ven afectados. En otras palabras, si su aplicación procesa rutinariamente conjuntos de resultados cortos con pocas filas, crear, leer y cerrar un cursor de servidor para cada conjunto de resultados, se usará más recursos de cliente y servidor de que es el caso donde el  **selectMethod** no está establecido en **cursor**.  
  
-   Lea los grandes de texto o valores binarios como flujos mediante el getAsciiStream, el getBinaryStream o los métodos getCharacterStream en lugar de la getBlob o los métodos de getClob. A partir de la versión 1.2, el [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) clase proporciona nueva get\<tipo > transmitir métodos para este propósito.  
  
-   Asegúrese de que las columnas con valores potencialmente grandes se colocan en último lugar en la lista de columnas en una instrucción SELECT y que get\<tipo > transmitir los métodos de la [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) se usan para tener acceso a las columnas de la orden en que se seleccionan.  
  
-   Asegúrese de que los parámetros OUT con valores potencialmente grandes se declaran en último lugar en la lista de parámetros en la instrucción SQL utilizada para crear el [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md). Además, asegúrese de que get\<tipo > transmitir los métodos de la [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) se usan para tener acceso a los parámetros OUT en el orden en que se declaran.  
  
-   Evite ejecutar simultáneamente más de una instrucción en la misma conexión. Ejecutar otra instrucción antes de procesar los resultados de la anterior puede provocar que los resultados sin procesar se almacenen en el búfer en la memoria de la aplicación.  
  
-   Hay algunos casos donde utilizando **selectMethod = cursor** en lugar de **responseBuffering = adaptive** sería más beneficioso, como:  
  
    -   Si su aplicación procesa solo avance, solo lectura conjunto de resultados lentamente, como la lectura de cada fila después de alguna entrada del usuario, con **selectMethod = cursor** en lugar de **responseBuffering = adaptive** podría ayudar a reducir el uso de recursos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    -   Si su aplicación procesa dos o más de solo avance de solo lectura conjuntos de resultados a la vez en la misma conexión, usando **selectMethod = cursor** en lugar de **responseBuffering = adaptive** podría ayudar a reducir la memoria necesaria para el controlador mientras procesa estos conjuntos de resultados.  
  
     En ambos casos, necesita considerar la sobrecarga de crear, leer y cerrar los cursores de servidor.  
  
 Además, la siguiente lista proporciona algunas recomendaciones para los conjuntos de resultados desplazables y actualizables de solo avance:  
  
-   Para conjuntos de resultados desplazables, cuando se captura un bloque de filas el controlador siempre lee en la memoria el número de filas indicado por la [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) método de la [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) de objetos, incluso cuando el almacenamiento en búfer adaptable está habilitada. Si el desplazamiento produce un OutOfMemoryError, puede reducir el número de filas recuperadas mediante una llamada a la [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) método de la [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) objeto para establecer el tamaño de captura en un número más pequeño de filas, incluso una sola 1 fila, si es necesario. Si esto no evita que un OutOfMemoryError, evite incluir columnas muy grandes en los conjuntos de resultados desplazables.  
  
-   Para los conjuntos de resultados adaptables de solo avance, cuando se captura un bloque de filas el controlador normalmente lee en la memoria el número de filas indicado por la [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) método de la [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) objeto, incluso cuando el búfer adaptable esté habilitado en la conexión. Si llama a la [siguiente](../../connect/jdbc/reference/next-method-sqlserverresultset.md) método de la [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) los resultados de objetos en un OutOfMemoryError, puede reducir el número de filas recuperadas mediante una llamada a la [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) método de la [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) objeto para establecer el tamaño de captura en un menor número de filas, incluso una sola 1 fila, si es necesario. También puede forzar el controlador no almacene en búfer todas las filas mediante una llamada a la [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método de la [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) objeto con "**adaptable**" parámetro antes de ejecutar la instrucción. Dado que el conjunto de resultados no es desplazable, si la aplicación obtiene acceso a un valor de columna grande utilizando uno de get\<tipo > métodos de secuencia, el controlador descarta el valor en cuanto la aplicación lo lee igual que lo hace para solo avance de solo lectura conjuntos de resultados.  
  
## <a name="see-also"></a>Vea también  
 [Mejora del rendimiento y confiabilidad con el controlador JDBC](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  


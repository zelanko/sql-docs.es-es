---
title: Empleo de almacenamiento en búfer adaptable
description: Descubra cómo el uso del almacenamiento en búfer adaptable elimina la sobrecarga de los cursores de servidor al recuperar datos de valores grandes mediante Microsoft JDBC Driver para SQL Server.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 92d4e3be-c3e9-4732-9a60-b57f4d0f7cb7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7f0e31c679ab1c85e5bbee9f3e66336c20e86521
ms.sourcegitcommit: 2600a414c321cfd6dc6daf5b9bcbc9a99c049dc4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603398"
---
# <a name="using-adaptive-buffering"></a>Empleo de almacenamiento en búfer adaptable

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

El almacenamiento en búfer adaptable está diseñado para recuperar cualquier tipo de datos de valores grandes sin sufrir la sobrecarga de los cursores de servidor. Las aplicaciones pueden usar la característica de almacenamiento en búfer adaptable con todas las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que son compatibles con el controlador.

Normalmente, cuando el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ejecuta una consulta, lleva todos los resultados del servidor a la memoria de la aplicación. Aunque este enfoque reduce el uso de recursos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede iniciar un OutOfMemoryError en la aplicación JDBC para las consultas que producen resultados muy grandes.

Para permitir que las aplicaciones administren resultados muy grandes, el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona almacenamiento en búfer adaptable. Con el almacenamiento en búfer adaptable, el controlador recupera los resultados de la ejecución de una instrucción de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a medida que la aplicación los necesita, en lugar de todos a la vez. El controlador también descarta los resultados en cuanto la aplicación ya no puede tener acceso a ellos. Se incluyen a continuación algunos ejemplos en los que el almacenamiento en búfer adaptable puede ser útil:

- **La consulta genera un conjunto de resultados muy amplio:** la aplicación puede ejecutar una instrucción SELECT que genera más filas de las que la aplicación puede almacenar en la memoria. En las versiones anteriores, la aplicación tenía que utilizar un cursor de servidor para evitar un OutOfMemoryError. El almacenamiento en búfer adaptable permite hacer un paso de solo lectura y solo avance de un conjunto de resultados arbitrariamente grande sin requerir un cursor de servidor.

- **La consulta genera columnas grandes de** [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) **o** [valores de parámetro OUT](../../connect/jdbc/reference/sqlservercallablestatement-class.md) de **SQLServerCallableStatement:** La aplicación puede recuperar un valor único (columna o el parámetro OUT) que es demasiado grande como para que quepa completamente en la memoria de la aplicación. El almacenamiento en búfer adaptable permite a la aplicación cliente recuperar este valor como un flujo, utilizando los métodos getAsciiStream, getBinaryStreamo o getCharacterStream. La aplicación recupera el valor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando lee del flujo.

> [!NOTE]  
> Con el almacenamiento en búfer adaptable, el controlador JDBC solamente almacena en búfer las cantidad de datos que debe almacenar. El controlador no proporciona un método público para controlar o limitar el tamaño del búfer.

## <a name="setting-adaptive-buffering"></a>Establecer el almacenamiento en búfer adaptable

A partir de Microsoft JDBC Driver 2.0, el comportamiento predeterminado del controlador es "**adaptive**". Dicho de otro modo, para obtener el comportamiento de almacenamiento en búfer adaptable, su aplicación no tiene que solicitar explícitamente el comportamiento adaptable. Pero, en la versión 1.2, el modo del almacenamiento en búfer era **full** de manera predeterminada y la aplicación tenía que solicitar el modo de almacenamiento en búfer adaptable explícitamente.

Hay tres formas en las que una aplicación puede solicitar que la ejecución de una instrucción deba usar el almacenamiento en búfer adaptable:

- La aplicación puede establecer la propiedad de conexión **responseBuffering** en "adaptive". Para más información sobre cómo configurar las propiedades de conexión, consulte [Establecimiento de las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).

- La aplicación puede utilizar el método [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md) del objeto [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) para establecer el modo de almacenamiento en búfer de respuesta para todas las conexiones creadas a través de ese objeto [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md).

- La aplicación puede utilizar el método [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) de la clase [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) para establecer el modo de almacenamiento en búfer de respuestas para un objeto de una instrucción determinada.

Al usar la versión 1.2 del controlador JDBC, la aplicación debe convertir el objeto de la instrucción en una clase [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) para utilizar el método [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md). En los ejemplos de código de [Lectura de ejemplo de datos grandes](../../connect/jdbc/reading-large-data-sample.md) y [Lectura de datos grandes con un ejemplo de procedimientos almacenados](../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md) se muestra este uso anterior.

Pero, con la versión 2.0 del controlador JDBC, las aplicaciones pueden usar el método [isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) y el método [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) para acceder a la funcionalidad específica del proveedor sin ninguna suposición sobre la jerarquía de clases de la implementación. Para ver un código de ejemplo, consulte el tema [Actualización de ejemplo de datos grandes](../../connect/jdbc/updating-large-data-sample.md).

## <a name="retrieving-large-data-with-adaptive-buffering"></a>Recuperar datos grandes con el almacenamiento en búfer adaptable

Cuando se leen valores grandes una vez con los métodos get\<Type>Stream y se tiene acceso a las columnas ResultSet y a los parámetros OUT CallableStatement en el orden que devuelve [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el almacenamiento en búfer adaptable reduce la utilización de memoria de la aplicación al procesar los resultados. Al utilizar el almacenamiento en búfer adaptable:

- Los métodos get\<Type>Stream definidos en las clases [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) y [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) devuelven secuencias de una sola lectura de forma predeterminada, aunque se pueden restablecer las secuencias si lo determina la aplicación. Si la aplicación quiere `reset` el flujo, tiene que llamar primero al método `mark` en ese flujo.

- Los métodos get\<Type>Stream definidos en las clases [SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md) y [SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md) devuelven secuencias cuya posición siempre se puede cambiar a la posición inicial de la secuencia sin llamar al método `mark`.

Cuando la aplicación utiliza el almacenamiento en búfer adaptable, los valores recuperados por los métodos get\<Type>Stream solo se pueden recuperar una vez. Si intenta llamar a cualquier método get\<Type> en la misma columna o parámetro después de llamar al método get\<Type>Stream del mismo objeto, se produce una excepción con el mensaje "Se obtuvo acceso a los datos y estos no están disponibles para esta columna o parámetro".

> [!NOTE]
> Una llamada a ResultSet.close() en pleno procesamiento de un conjunto ResultSet requeriría que Microsoft JDBC Driver para SQL Server leyese y descartase todos los paquetes restantes. Esto puede tardar un tiempo sustancial si la consulta ha devuelto un conjunto de datos grandes y, sobre todo, si la conexión de red es lenta.

## <a name="guidelines-for-using-adaptive-buffering"></a>Directrices para el uso del almacenamiento en búfer adaptable

Los desarrolladores de software deberían seguir estas importantes directrices para disminuir la utilización de memoria por parte de la aplicación:

- Evite utilizar la propiedad de cadena de conexión **selectMethod=cursor** para permitir a la aplicación procesar un conjunto de resultados muy grande. La característica de almacenamiento en búfer adaptable permite a las aplicaciones procesar los conjuntos de resultados de solo avance y solo lectura muy grandes sin utilizar un cursor de servidor. Tenga en cuenta que cuando configura **selectMethod=cursor**, se ven impactados todos los conjuntos de resultados de solo avance y solo lectura producidos por esa conexión. Dicho de otro modo, si la aplicación procesa rutinariamente conjuntos de resultados cortos con pocas filas, crear, leer y cerrar un cursor de servidor por cada conjunto de resultados usará más recursos del lado cliente y en el lado servidor de lo que sucede cuando **selectMethod** no está configurado en **cursor**.

- Lea valores binarios o de texto grandes como flujos mediante los métodos getAsciiStream, getBinaryStream o getCharacterStream en lugar de los métodos getBlob o getClob. A partir de la versión 1.2, la clase [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) proporciona nuevos métodos get\<Type>Stream para este fin.

- Asegúrese de que las columnas con valores potencialmente grandes se colocan en último lugar en la lista de columnas en una instrucción SELECT y de que se usan los métodos get\<Type>Stream de [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) para acceder a las columnas en el orden en que se seleccionan.

- Asegúrese de que los parámetros OUT con valores potencialmente grandes se declaran en último lugar en la lista de parámetros del código SQL que se usa para crear [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md). Además, compruebe que los métodos get\<Type>Stream de [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) se usan para acceder a los parámetros OUT en el orden en que se declaran.

- Evite ejecutar simultáneamente más de una instrucción en la misma conexión. Ejecutar otra instrucción antes de procesar los resultados de la anterior puede provocar que los resultados sin procesar se almacenen en el búfer en la memoria de la aplicación.

- Hay algunos casos en los que el uso de **selectMethod=cursor** en lugar de **responseBuffering=adaptive** sería más beneficioso, como:

  - Si su aplicación procesa lentamente un conjunto de resultados de solo avance y solo lectura, como la lectura de cada fila después de alguna entrada del usuario, utilizar **selectMethod=cursor** en lugar de **responseBuffering=adaptive** puede ayudar a reducir el uso de recursos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

  - Si la aplicación procesa dos o más conjuntos de resultados de solo avance y solo lectura al mismo tiempo en la misma conexión, utilizar **selectMethod=cursor** en lugar de **responseBuffering=adaptive** podría ayudar a reducir la memoria necesaria para el controlador mientras procesa estos conjuntos de resultados.

  En ambos casos, necesita considerar la sobrecarga de crear, leer y cerrar los cursores de servidor.

Además, la siguiente lista proporciona algunas recomendaciones para los conjuntos de resultados desplazables y actualizables de solo avance:

- Para los conjuntos de resultados desplazables, cuando recupera un conjunto de filas el controlador siempre lee en la memoria el número de filas indicado por el método [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) del objeto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md), incluso aunque esté habilitado el almacenamiento en búfer adaptable. Si el desplazamiento produce un OutOfMemoryError, puede reducir el número de filas recuperadas llamando al método [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) del objeto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) para configurar el tamaño de captura en un número de filas más pequeño, incluso una sola fila si es necesario. Si esto no impide un OutOfMemoryError, evite incluir columnas muy grandes en los conjuntos de resultados desplazables.

- Para los conjuntos de resultados de solo avance, cuando recupera un conjunto de filas el controlador normalmente lee en la memoria el número de filas indicado por el método [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) del objeto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md), incluso aunque el almacenamiento en búfer adaptable esté habilitado en la conexión. Si la llamada al método [next](../../connect/jdbc/reference/next-method-sqlserverresultset.md) del objeto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) produce un OutOfMemoryError, puede reducir el número de filas recuperadas llamando al método [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) del objeto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) para configurar el tamaño de captura en un número de filas más pequeño, incluso una sola fila si es necesario. También puede forzar el controlador para que no almacene filas en el almacenamiento den búfer llamando al método [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) del objeto [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) con el parámetro "**adaptive**" antes de ejecutar la instrucción. Como el conjunto de resultados no es desplazable, si la aplicación accede a un número de columna grande utilizando uno de los métodos get\<Type>Stream, el controlador rechaza el valor en cuanto la aplicación lo lee, lo mismo que hace con los conjuntos de resultados de solo avance y solo lectura.

## <a name="see-also"></a>Consulte también

[Mejora del rendimiento y la confiabilidad con el controlador JDBC](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)

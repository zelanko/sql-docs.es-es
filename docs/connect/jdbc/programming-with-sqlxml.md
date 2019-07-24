---
title: Programar con SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4d2cc57c-7293-4d92-b8b1-525e2b35f591
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c8d88f6c9febf582aa9aca3d47931ceb72074c87
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956172"
---
# <a name="programming-with-sqlxml"></a>Programar con SQLXML
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  En esta sección se describe cómo usar los métodos de la API del [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] para almacenar y recuperar un documento XML en y desde una base de datos relacional con objetos **SQLXML**.  
  
 Esta sección también contiene información acerca de los tipos de objetos SQLXML y proporciona una lista de las instrucciones y las limitaciones importantes cuando se usan objetos SQLXML.  
  
## <a name="reading-and-writing-xml-data-with-sqlxml-objects"></a>Leer y escribir datos XML con objetos SQLXML  
 En la lista siguiente se describe cómo usar los métodos de la API del [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] para leer y escribir datos XML con objetos SQLXML:  
  
-   Para crear un objeto SQLXML, use el método [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). Tenga en cuenta que este método crea un objeto SQLXML sin dato alguno. Para agregar datos **XML** a un objeto SQLXML, llame a uno de los métodos siguientes especificados en la interfaz SQLXML: SetResult, SetCharacterStream, SetBinaryStream o setString.  
  
-   Para recuperar el propio objeto SQLXML, use los métodos getSQLXML de la clase [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) o de la clase [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md).  
  
-   Para recuperar los datos **XML** de un objeto SQLXML, utilice uno de los métodos siguientes que se especifican en la interfaz SQLXML: GetSource, GetCharacterStream, GetBinaryStream o GetString.  
  
-   Para actualizar los datos **xml** de un objeto SQLXML, use el método [updateSQLXML](../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md) de la clase [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
-   Para almacenar un objeto SQLXML en una columna de tabla del tipo **xml**, use los métodos setSQLXML de la clase [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) o de la clase [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md).  
  
 El código muestra de [Ejemplo de tipo de datos SQLXML](../../connect/jdbc/sqlxml-data-type-sample.md) muestra cómo realizar estas tareas API comunes.  
  
## <a name="readable-and-writable-sqlxml-objects"></a>Objetos SQLXML de lectura y escritura  
 La tabla siguiente enumera qué tipos de objetos SQLXML son compatibles con los métodos establecedor, captador y actualizador de la API de JDBC. Las columnas de la tabla hacen referencia a lo siguiente:  
  
-   La columna **Nombre de método** enumera los métodos compatibles establecedor, captador y actualizador de la API de JDBC.  
  
-   La columna **Objeto SQLXML de captador** representa un objeto SQLXML que es creado bien por el método [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md) de la clase [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) o bien por el método [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) de la clase [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
-   La columna **Objeto SQLXML establecedor** representa un objeto SQLXML que es creado por el método [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). Tenga en cuenta que los métodos establecedor que se indican abajo solamente aceptan un objeto SQLXML creado por el método [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md).  
  
|Nombre de método|Objeto SQLXML de captador<br /><br /> (lectura)|Objeto SQLXML establecedor<br /><br /> (escritura)|  
|-----------------|-------------------------------------------|-------------------------------------------|  
|CallableStatement.setSQLXML()|No admitida|Admitida|  
|CallableStatement.setObject()|No admitida|Admitida|  
|PreparedStatement.setSQLXML()|No admitida|Admitida|  
|PreparedStatement.setObject()|No admitida|Admitida|  
|ResultSet.updateSQLXML()|No admitida|Admitida|  
|ResultSet.updateObject()|No admitida|Admitida|  
|ResultSet.getSQLXML()|Admitida|No admitida|  
|CallableStatement.getSQLXML()|Admitida|No admitida|  
  
 Tal como se muestra en el área superior, los métodos SQLXML establecedor no funcionarán con los objetos SQLXML de lectura; similarmente, los métodos captadores no funcionarán con los objetos SQLXML de escritura.  
  
 Si la aplicación invoca el método setObject especificando un parámetro de escala o de longitud con un objeto SQLXML, se ignora el parámetro de escala o de longitud.  
  
## <a name="guidelines-and-limitations-when-using-sqlxml-objects"></a>Instrucciones y limitaciones cuando se usan objetos SQLXML  
 Las aplicaciones pueden usar objetos SQLXML para leer datos XML de la base de datos y para escribirlos en ella. La lista siguiente proporciona información relativa a las instrucciones y limitaciones específicas durante el uso de objetos SQLXML.  
  
-   Un objeto SQLXML solamente puede ser válido durante la transacción en la que se creó.  
  
-   Un objeto SQLXML recibido de un método de captador solamente se puede usar para leer datos.  
  
-   Un objeto SQLXML creado por el objeto de conexión solamente se puede usar para escribir datos.  
  
-   La aplicación solamente puede invocar un método de captador en un objeto SQLXML de lectura para leer datos. Después de invocarse el método de captador, todos los demás métodos captador o establecedor del mismo objeto SQLXML dan error.  
  
-   La aplicación solamente puede invocar el método free en el objeto SQLXML después de que se ha leído o escrito. Sin embargo, sigue siendo posible procesar el flujo o el origen devueltos mientras la columna o el parámetro subyacentes estén activos. Si la columna o el parámetro subyacentes están inactivos, el flujo o el origen asociados con el objeto SQLXML se cerrarán. Si la columna o el parámetro subyacentes ya no son válidos, los datos subyacentes ya no estarán disponibles para los métodos captadores de Stream, Simple API for XML (SAX) y de Streaming API for XML (StAX).  
  
-   La aplicación solamente puede invocar un método establecedor en un objeto SQLXML de escritura. Después de invocarse el método establecedor, todos los demás métodos establecedor o captador del mismo objeto SQLXML dan error.  
  
-   Para establecer datos en el objeto SQLXML, la aplicación debe usar las funciones y el método establecedor apropiados en el objeto devuelto.  
  
-   Los métodos getSQLXML de la clase [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) y de la clase [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) devuelven datos **null** si la columna subyacente es **null**.  
  
-   Los objetos establecedor pueden ser válidos durante la conexión en la que son creados.  
  
-   A las aplicaciones no se les permite establecer un valor **NULL** utilizando los métodos establecedor proporcionados por la interfaz de SQLXML. Las aplicaciones pueden establecer un valor vacío ("") utilizando los métodos establecedor proporcionados por la interfaz de SQLXML. Para establecer un valor **null**, las aplicaciones deberían llamar a uno de los elementos siguientes:  
  
    -   Los métodos setNull de la clase [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) y de la clase [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).  
  
    -   Los métodos setObject de la clase [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) y de la clase [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).  
  
    -   Los métodos setSQLXML de la clase [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) y de la clase [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) con un valor de parámetro **null**.  
  
-   Al trabajar con documentos XML, recomendamos usar los analizadores Simple API for XML (SAX) y Streaming API for XML (StAX) en lugar de los analizadores de Document Object Model (DOM) por motivos de rendimiento.  
  
 Los analizadores XML no pueden controlar valores vacíos. Sin embargo, SQL Server permite que las aplicaciones recuperen valores vacíos de columnas de base de datos del tipo de datos XML y los almacenen en ellas. Eso significa que al analizar los datos XML, si el valor subyacente está vacío, el analizador devuelve una excepción. En los resultados de DOM, el controlador JDBC capta esa excepción y devuelve un error. En los resultados de SAX y Stax, el error procede directamente del analizador.  
  
## <a name="adaptive-buffering-and-sqlxml-support"></a>Almacenamiento en búfer adaptable y compatibilidad con SQLXML  
 Los flujos binarios y de caracteres devueltos por el objeto SQLXML obedecen a los modos de almacenamiento en búfer completo o adaptable. Por otra parte, si los analizadores XML no son secuencia, no obedecerán a los valores completos o adaptables. Para obtener más información sobre el almacenamiento en búfer adaptable, vea [usar el almacenamiento en búfer adaptable](../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="see-also"></a>Consulte también  
 [Compatibilidad con datos XML](../../connect/jdbc/supporting-xml-data.md)  
  
  

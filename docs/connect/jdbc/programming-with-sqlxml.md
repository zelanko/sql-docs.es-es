---
title: Programar con SQLXML | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4d2cc57c-7293-4d92-b8b1-525e2b35f591
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e5cb6d2d44b9988dda28d5e9bd10db0d96467ff6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="programming-with-sqlxml"></a>Programar con SQLXML
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Esta sección describe cómo utilizar el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] métodos de la API para almacenar y recuperar un documento XML de documentos en y desde una base de datos relacional con **SQLXML** objetos.  
  
 Esta sección también contiene información acerca de los tipos de objetos SQLXML y proporciona una lista de las instrucciones y las limitaciones importantes cuando se usan objetos SQLXML.  
  
## <a name="reading-and-writing-xml-data-with-sqlxml-objects"></a>Leer y escribir datos XML con objetos SQLXML  
 En la lista siguiente describe cómo usar el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] métodos de la API para leer y escribir datos XML con objetos SQLXML:  
  
-   Para crear un objeto SQLXML, use la [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) método de la [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) clase. Tenga en cuenta que este método crea un objeto SQLXML sin dato alguno. Para agregar **xml** datos al objeto SQLXML, llame a uno de los métodos siguientes que se especifican en la interfaz SQLXML: setResult, setCharacterStream, setBinaryStream, o setString.  
  
-   Para recuperar el propio objeto SQLXML, use los métodos de getSQLXML de la [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) clase o la [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) clase.  
  
-   Para recuperar el **xml** datos de un objeto SQLXML, utilice uno de los métodos siguientes que se especifican en la interfaz SQLXML: getSource, getCharacterStream, getBinaryStream, o getString.  
  
-   Para actualizar la **xml** datos en un objeto SQLXML, use la [updateSQLXML](../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md) método de la [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) clase.  
  
-   Para almacenar un objeto SQLXML en una columna de tabla de base de datos de tipo **xml**, use los métodos setSQLXML de la [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) clase o la [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)clase.  
  
 El código de ejemplo de [ejemplo de tipo de datos de SQLXML](../../connect/jdbc/sqlxml-data-type-sample.md) muestra cómo realizar estas tareas API comunes.  
  
## <a name="readable-and-writable-sqlxml-objects"></a>Objetos SQLXML de lectura y escritura  
 La tabla siguiente enumera qué tipos de objetos SQLXML son compatibles con los métodos establecedor, captador y actualizador de la API de JDBC.  Las columnas de la tabla hacen referencia a lo siguiente:  
  
-   El **nombre del método** columna muestra los métodos de captador, establecedor y actualizador admitidos en la API de JDBC.  
  
-   El **objeto SQLXML de captador** columna representa un objeto SQLXML, que se creó mediante el el [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md) método de la [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) clase o el [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) método de la [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) clase.  
  
-   El **objeto SQLXML establecedor** columna representa un objeto SQLXML, que es creado por el [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) método de la [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) clase. Tenga en cuenta que los métodos de establecedor siguientes aceptan solo un objeto SQLXML creado por el [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) método.  
  
|Nombre de método|Objeto SQLXML de captador<br /><br /> (lectura)|Objeto SQLXML establecedor<br /><br /> (escritura)|  
|-----------------|-------------------------------------------|-------------------------------------------|  
|CallableStatement.setSQLXML()|No se admite|Compatible|  
|CallableStatement.setObject()|No se admite|Compatible|  
|PreparedStatement.setSQLXML()|No se admite|Compatible|  
|PreparedStatement.setObject()|No se admite|Compatible|  
|ResultSet.updateSQLXML()|No se admite|Compatible|  
|ResultSet.updateObject()|No se admite|Compatible|  
|ResultSet.getSQLXML()|Compatible|No se admite|  
|CallableStatement.getSQLXML()|Compatible|No se admite|  
  
 Tal como se muestra en el área superior, los métodos SQLXML establecedor no funcionarán con los objetos SQLXML de lectura; similarmente, los métodos captadores no funcionarán con los objetos SQLXML de escritura.  
  
 Si la aplicación invoca el método setObject especificando una escala o un parámetro de longitud con un objeto SQLXML, se omite el parámetro de escala o longitud.  
  
## <a name="guidelines-and-limitations-when-using-sqlxml-objects"></a>Instrucciones y limitaciones cuando se usan objetos SQLXML  
 Las aplicaciones pueden usar objetos SQLXML para leer datos XML de la base de datos y para escribirlos en ella. La lista siguiente proporciona información relativa a las instrucciones y limitaciones específicas durante el uso de objetos SQLXML.  
  
-   Un objeto SQLXML solamente puede ser válido durante la transacción en la que se creó.  
  
-   Un objeto SQLXML recibido de un método de captador solamente se puede usar para leer datos.  
  
-   Un objeto SQLXML creado por el objeto de conexión solamente se puede usar para escribir datos.  
  
-   La aplicación solamente puede invocar un método de captador en un objeto SQLXML de lectura para leer datos. Después de invocarse el método de captador, todos los demás métodos captador o establecedor del mismo objeto SQLXML dan error.  
  
-   La aplicación puede invocar solo el método libre en el objeto SQLXML después de que se leen o escriben en. Sin embargo, sigue siendo posible procesar el flujo o el origen devueltos mientras la columna o el parámetro subyacentes estén activos. Si la columna o el parámetro subyacentes están inactivos, el flujo o el origen asociados con el objeto SQLXML se cerrarán. Si la columna o el parámetro subyacentes ya no son válidos, los datos subyacentes ya no estarán disponibles para los métodos captadores de Stream, Simple API for XML (SAX) y de Streaming API for XML (StAX).  
  
-   La aplicación solamente puede invocar un método establecedor en un objeto SQLXML de escritura. Después de invocarse el método establecedor, todos los demás métodos establecedor o captador del mismo objeto SQLXML dan error.  
  
-   Para establecer datos en el objeto SQLXML, la aplicación debe usar las funciones y el método establecedor apropiados en el objeto devuelto.  
  
-   Los métodos de getSQLXML de la [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) clase y la [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) clase devuelve **null** datos si la columna subyacente es **null**.  
  
-   Los objetos establecedor pueden ser válidos durante la conexión en la que son creados.  
  
-   Las aplicaciones no se permiten establecer un **null** valor mediante el uso de los métodos establecedor proporcionados por la interfaz SQLXML. Las aplicaciones pueden establecer un valor vacío ("") utilizando los métodos establecedor proporcionados por la interfaz de SQLXML. Para establecer un **null** valor, las aplicaciones deberían llamar a uno de los siguientes valores:  
  
    -   Los métodos setNull de la [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) clase y [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) clase.  
  
    -   Los métodos setObject de la [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) clase y [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) clase.  
  
    -   Los métodos setSQLXML de la [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) clase y [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) clase con un **null** el valor del parámetro.  
  
-   Al trabajar con documentos XML, recomendamos usar los analizadores Simple API for XML (SAX) y Streaming API for XML (StAX) en lugar de los analizadores de Document Object Model (DOM) por motivos de rendimiento.  
  
 Los analizadores XML no pueden controlar valores vacíos. Sin embargo, SQL Server permite que las aplicaciones recuperen valores vacíos de columnas de base de datos del tipo de datos XML y los almacenen en ellas. Eso significa que al analizar los datos XML, si el valor subyacente está vacío, el analizador devuelve una excepción. En los resultados de DOM, el controlador JDBC capta esa excepción y devuelve un error. En los resultados de SAX y Stax, el error procede directamente del analizador.  
  
## <a name="adaptive-buffering-and-sqlxml-support"></a>Almacenamiento en búfer adaptable y compatibilidad con SQLXML  
 Los flujos binarios y de caracteres devueltos por el objeto SQLXML obedecen a los modos de almacenamiento en búfer completo o adaptable. Por otra parte, si los analizadores XML no son secuencia, no obedecerán a los valores completos o adaptables. Para obtener más información sobre el almacenamiento en búfer adaptable, vea [usar almacenamiento en búfer adaptable](../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con datos XML](../../connect/jdbc/supporting-xml-data.md)  
  
  

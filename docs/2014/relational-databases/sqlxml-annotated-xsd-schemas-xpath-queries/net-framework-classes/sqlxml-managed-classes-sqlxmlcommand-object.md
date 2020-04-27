---
title: Objeto SqlXmlCommand (clases administradas de SQLXML) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- void ExecuteNonQuery() method
- namespaces property
- Stream ExecuteStream() method
- CommandType property
- RootTag property
- OutputEncoding property
- XmlReader ExecuteXmlReader() method
- Managed Classes [SQLXML], SqlXmlCommand object
- SQLXML Managed Classes, SqlXmlCommand object
- Base Path property
- void ClearParameters() method
- public void ExecuteToStream(Stream outputStream) method
- SqlXmlCommand object
- CommandText property
- XslPath property
- SchemaPath property
- SqlXmlParameter CreateParameter() method
- ClientSideXML property
- CommandStream property
ms.assetid: c1f9e0bb-a89d-4d6a-a96e-289ef516a3a6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d002208a83b58a4c8547bc6ce85db073ced70974
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66010741"
---
# <a name="sqlxmlcommand-object-sqlxml-managed-classes"></a>Objeto SqlXmlCommand (clases administradas SQLXML)
  Este es el constructor del objeto SqlXmlCommand:  
  
```  
public SqlXmlCommand(string cnString)  
```  
  
 Donde `cnString` es la cadena de conexión ADO u OleDb que identifica el servidor, la base de datos y la información de inicio `Provider=SQLOLEDB; Server=(local); database=AdventureWorks; Integrated Security=SSPI"`de sesión (por ejemplo,).  
  
 En la cadena de conexión, `Provider` debe ser SQLOLEDB y `Data Provider` no debería incluirse en la cadena del proveedor.  
  
 Para obtener un ejemplo funcional, vea [ejecutar consultas SQL &#40;clases administradas de SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md).  
  
## <a name="methods"></a>Métodos  
 El objeto TheSqlXmlCommand admite varios métodos, incluidos los métodos siguientes para ejecutar un comando:  
  
 void ExecuteNonQuery ()  
 Ejecuta el comando pero no devuelve nada. Este método resulta de gran utilidad si desea ejecutar un comando nonquery (es decir, un comando que no devuelve nada). Un ejemplo sería ejecutar un diagrama de actualización (updategram) o diferencia (DiffGram) que actualiza registros pero que no devuelve nada.  
  
 Stream ExecuteStream ()  
 Devuelve un nuevo objeto de secuencia. Este método resulta de gran utilidad cuando desea que los resultados de la consulta se devuelvan en un nuevo flujo. Para obtener un ejemplo funcional, vea [ejecutar consultas SQL &#40;clases administradas de SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md).  
  
 public void ExecuteToStream (Stream outputStream)  
 Escribe los resultados de la consulta en un flujo existente. Este método es útil cuando se tiene un flujo al que se necesitan los resultados anexados (por ejemplo, para que los resultados de la consulta se escriban en System. Web. HttpResponse. OutputStream). Para obtener un ejemplo funcional, vea [ejecutar consultas SQL &#40;clases administradas de SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md).  
  
 XmlReader ExecuteXmlReader ()  
 Devuelve un objeto XmlReader. Puede usar este método para manipular directamente los datos en el objeto XmlReader o conectar la arquitectura encadenada de System. Xml. Para obtener más información, vea la documentación de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework. Para obtener un ejemplo funcional, vea [ejecutar consultas SQL mediante el método ExecuteXMLReader](executing-sql-queries-by-using-the-executexmlreader-method.md).  
  
 El objeto TheSqlXmlCommand también admite estos métodos adicionales:  
  
 SqlXmlParameter CreateParameter ()  
 Crea un objeto SqlXmlParameter. Puede establecer valores para los parámetros de *nombre* y *valor* de este objeto. Este método resulta de gran utilidad si desea pasar parámetros a un comando. Para obtener un ejemplo funcional, vea [ejecutar consultas SQL &#40;clases administradas de SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md).  
  
 void ClearParameters ()  
 Borra los parámetros creados para un objeto de comando determinado. Este método resulta de gran utilidad si desea ejecutar varias consultas en el mismo objeto de comando.  
  
## <a name="properties"></a>Propiedades  
 El objeto SqlXmlCommand también admite estas propiedades:  
  
 Clientsidexml,  
 Cuando se establece en True, especifica que la conversión del conjunto de filas a XML debe realizarse en el cliente en lugar de realizarse en el servidor. Esta propiedad resulta de gran utilidad si desea mover la carga de rendimiento al nivel intermedio. La propiedad también permite ajustar los procedimientos almacenados existentes con FOR XML para obtener la salida XML.  
  
 SchemaPath  
 Nombre del esquema de asignación junto con la ruta de acceso al directorio (por ejemplo, C:\x\y\MySchema.xml). Esta propiedad resulta muy útil para especificar un esquema de asignación para las consultas XPath. La ruta de acceso especificada puede ser absoluta o relativa. Si la ruta de acceso es relativa, la ruta de acceso base que se especifica en la ruta de acceso base se usa para resolver la ruta de acceso relativa. Si no se especifica ninguna ruta de acceso base, la ruta de acceso relativa es relativa al directorio actual. Para obtener un ejemplo funcional, vea [obtener acceso a la funcionalidad de SQLXML en el entorno de .net](accessing-sqlxml-functionality-in-the-net-environment.md).  
  
 XslPath  
 Nombre del archivo XSL junto con la ruta de acceso al directorio. La ruta de acceso especificada puede ser absoluta o relativa. Si la ruta de acceso es relativa, la ruta de acceso base que se especifica en la ruta de acceso base se usa para resolver la ruta de acceso relativa. Si no se especifica ninguna ruta de acceso base, la ruta de acceso relativa es relativa al directorio actual. Para obtener un ejemplo funcional, vea [aplicar una transformación XSL &#40;clases administradas de SQLXML&#41;](applying-an-xsl-transformation-sqlxml-managed-classes.md).  
  
 Ruta de base  
 Ruta de acceso base (ruta de acceso a un directorio). Esta propiedad es útil para resolver una ruta de acceso relativa que se especifica para un archivo XSL (mediante la propiedad XslPath), un archivo de esquema de asignación (mediante la propiedad SchemaPath) o una referencia de esquema externo en una plantilla XML (especificada mediante el `mapping-schema` atributo).  
  
 OutputEncoding  
 Especifica la codificación del flujo que se devuelve cuando se ejecuta el comando. Esta propiedad es útil para solicitar una codificación concreta para el flujo que se devuelve. Entre algunas de las codificaciones que más se usan se incluyen UTF-8, ANSI y Unicode. La codificación predeterminada es UTF-8.  
  
 Espacios de nombres  
 Habilita la ejecución de consultas XPath que usan espacios de nombres. Para obtener más información acerca de las consultas XPath con espacios de nombres, vea [ejecutar consultas XPath con espacios de nombres &#40;clases administradas de SQLXML&#41;](executing-xpath-queries-with-namespaces-sqlxml-managed-classes.md). Para obtener un ejemplo funcional, vea [ejecutar consultas XPath &#40;clases administradas de SQLXML&#41;](executing-xpath-queries-sqlxml-managed-classes.md).  
  
 RootTag  
 Proporciona el elemento raíz único para XML generado por la ejecución del comando. Un documento XML válido requiere una etiqueta de nivel raíz única. Si el comando ejecutado genera un fragmento XML (sin un elemento de nivel superior único) puede especificar un elemento raíz para el XML que se devuelve. Para obtener un ejemplo funcional, vea [aplicar una transformación XSL &#40;clases administradas de SQLXML&#41;](applying-an-xsl-transformation-sqlxml-managed-classes.md).  
  
 CommandText  
 Texto del comando. Esta propiedad se usa para especificar el texto del comando que se desea ejecutar. Para obtener un ejemplo funcional, vea [ejecutar consultas SQL &#40;clases administradas de SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md).  
  
 CommandStream  
 Secuencia de comandos. Esta propiedad resulta útil si desea ejecutar un comando desde un archivo (por ejemplo, una plantilla XML). Cuando se usa CommandStream, solo se admiten los valores de CommandType **"template"**, **"diagrama"** y **"DiffGram"** . Para obtener un ejemplo funcional, vea [ejecutar archivos de plantilla mediante la propiedad CommandStream](executing-template-files-by-using-the-commandstream-property.md).  
  
 CommandType  
 Identifica el tipo de comando. Esta propiedad se usa para especificar el tipo de comando que se desea ejecutar. Los valores de la tabla siguiente determinan el tipo del comando. Para obtener un ejemplo funcional, vea [obtener acceso a la funcionalidad de SQLXML en el entorno de .net](accessing-sqlxml-functionality-in-the-net-environment.md).  
  
|Value|Descripción|  
|-----------|-----------------|  
|SqlXmlCommandType. SQL|Ejecuta un comando SQL (por ejemplo, `SELECT * FROM Employees FOR XML AUTO`).|  
|SqlXmlCommandType. XPath|Ejecuta un comando XPath (por ejemplo, `Employees[@EmployeeID=1]`).|  
|SqlXmlCommandType. template|Ejecuta una plantilla XML.|  
|SqlXmlCommandType. TemplateFile|Ejecuta un archivo de plantilla en la ruta de acceso especificada.|  
|SqlXmlCommandType. diagrama|Ejecuta un diagrama de actualización (updategram).|  
|SqlXmlCommandType. DiffGram|Ejecuta un diagrama de diferencia (DiffGram).|  
  
## <a name="see-also"></a>Consulte también  
 [Objeto SqlXmlParameter &#40;clases administradas de SQLXML&#41;](sqlxml-managed-classes-sqlxmlparameter-object.md)   
 [Objeto SqlXmlAdapter &#40;clases administradas de SQLXML&#41;](sqlxml-managed-classes-sqlxmladapter-object.md)  
  
  

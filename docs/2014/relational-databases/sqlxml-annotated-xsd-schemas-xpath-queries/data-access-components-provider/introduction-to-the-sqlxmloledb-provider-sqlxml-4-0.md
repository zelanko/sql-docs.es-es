---
title: Introducción al proveedor SQLXMLOLEDB (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, properties
- adExecuteStream flag
- SQLXMLOLEDB Provider, about SQLXMLOLEDB Provider
ms.assetid: 2e3f3817-4209-4bf4-9f46-248c95bc6f1b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 63badb45984b754e8f586e30f2d659a840db5d43
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48134731"
---
# <a name="introduction-to-the-sqlxmloledb-provider-sqlxml-40"></a>Introducción al proveedor SQLXMLOLEDB (SQLXML 4.0)
  El proveedor SQLXMLOLEDB es un proveedor OLE DB que expone la funcionalidad de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML a través de objetos de datos ActiveX (ADO). Sin embargo, el proveedor solamente puede ejecutar comandos en el modo "escribir en un flujo de salida" de ADO. El proveedor SQLXMLOLEDB no es un proveedor de conjunto de filas. Cuando se ejecuta un comando, debe especificar la marca adExecuteStream, que indica a ADO que use el flujo de salida que ha especificado.  
  
 El ejemplo siguiente muestra la sintaxis para el comando Execute en el que se especifica el adExecuteStream, marca:  
  
```  
Dim oTestCommand As New ADODB.Command  
...  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Execute , , adExecuteStream  
...  
```  
  
## <a name="sqlxmloledb-provider-specific-properties"></a>Propiedades específicas del proveedor SQLXMLOLEDB  
 El proveedor SQLXMLOLEDB expone la siguiente propiedad de conexión específica del proveedor.  
  
|Conexión<br /><br /> propiedad|Default<br /><br /> (si existe)|Descripción|  
|-----------------------------|----------------------------|-----------------|  
|Proveedor de datos||Proporciona el PROGID del proveedor OLE DB a través del que SQLXMLOLEDB ejecuta los comandos. A partir de SQLXML 4.0 y [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], este proveedor se incluye con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client; por lo tanto, este valor de propiedad se restringe a "SQLNCLI11". Para obtener más información, vea [Programación de SQL Server Native Client](../../native-client/sql-server-native-client-programming.md).|  
  
 El proveedor SQLXMLOLEDB expone las siguientes propiedades de comando específicas del proveedor.  
  
|Comando<br /><br /> propiedad|Default<br /><br /> (si existe)|Descripción|  
|--------------------------|----------------------------|-----------------|  
|Ruta de acceso base|""|Especifica la ruta de acceso del archivo base. La ruta de acceso del archivo base se usa para especificar la ubicación del lenguaje de hojas de estilo XML (XSL) o de los archivos de esquema de asignación. La ruta de acceso del archivo base también se usa para resolver las rutas de acceso relativas de XSL o de asignación de archivos de esquema que se han especificado en las propiedades del esquema de asignación o XSL.<br /><br /> Para obtener un ejemplo en el que se utiliza esta propiedad, vea [ejecutar consultas XPath &#40;proveedor SQLXMLOLEDB&#41;](executing-xpath-queries-sqlxmloledb-provider.md).|  
|ClientSideXML|False|Establezca esta propiedad en True si desea que el proceso de conversión del conjunto de filas a XML se produzca en el cliente en lugar de en el servidor. Esto resulta de gran utilidad si desea mover la carga de rendimiento al nivel intermedio.<br /><br /> Para obtener un ejemplo en el que se utiliza esta propiedad, vea [Executing SQL Queries &#40;proveedor SQLXMLOLEDB&#41; ](executing-sql-queries-sqlxmloledb-provider.md) o [ejecutar plantillas que contienen consultas SQL &#40;proveedor SQLXMLOLEDB&#41; ](executing-templates-that-contain-sql-queries-sqlxmloledb-provider.md).|  
|Tipo de contenido||Devuelve el tipo de contenido de salida. Esta propiedad es de solo lectura (READ ONLY).<br /><br /> Esta propiedad proporciona información al explorador acerca del tipo de contenido (como TEXT/XML, TEXT/HTML, imagen/jpeg, etc.). El valor de esta propiedad se convierte en el **contenido-tipo** campo que se envía al explorador como parte del encabezado HTTP, que contiene el tipo MIME (Multipurpose Internet Mail Extensions) del documento que se envían como el cuerpo.|  
|Esquema de asignación|NULL|Si una aplicación cliente ejecuta una consulta XPath en un esquema de asignación (XDR o XSD), esta propiedad se usa para especificar el nombre del esquema de asignación.<br /><br /> La ruta de acceso especificada puede ser relativa (xyz/abc/MySchema.xml) o absoluta (C:\miCarpeta\abc\MySchema.xml).<br /><br /> Si se especifica una ruta de acceso relativa, se utiliza la ruta de acceso base especificada por la propiedad de ruta de acceso Base para resolver la ruta de acceso relativa. Si no se ha especificado ninguna ruta de acceso en la propiedad de ruta de acceso Base, la ruta de acceso relativa es relativa al directorio actual.<br /><br /> Al especificar un valor para la propiedad de esquema de asignación, puede especificar una ruta de acceso del directorio local o una dirección URL (http://...). Si especifica una dirección URL, debe configurar WinHTTP para obtener acceso a los servidores HTTP y HTTPS a través de un servidor proxy. Puede hacerlo ejecutando la utilidad Proxycfg.exe. Para obtener más información, vea el tema sobre la forma de usar la utilidad de configuración del proxy WinHTTP en MSDN Library.<br /><br /> Para obtener un ejemplo en el que se utiliza esta propiedad, vea [ejecutar consultas XPath &#40;proveedor SQLXMLOLEDB&#41;](executing-xpath-queries-sqlxmloledb-provider.md).|  
|espacios de nombres||Esta propiedad habilita la ejecución de consultas XPath que usan espacios de nombres. Para obtener un ejemplo en el que se utiliza esta propiedad, vea [ejecutar consultas XPath con espacios de nombres &#40;proveedor SQLXMLOLEDB&#41;](executing-xpath-queries-with-namespaces-sqlxmloledb-provider.md).|  
|ss Stream Flags||Esta propiedad se usa para especificar tipos determinados de restricciones de seguridad. Por ejemplo, es posible que no desee permitir referencias URL a archivos o rutas de acceso absolutas a archivos (como sitios externos). O bien, puede que no desee permitir consultas en las plantillas.<br /><br /> La propiedad puede asignarse a estos valores:<br /><br /> 1 = STREAM_FLAGS_DISALLOW_URL 2 = STREAM_FLAGS_DISALLOW_ABSOLUTE_PATH 4 = STREAM_FLAGS_DISALLOW_QUERY A 8 = STREAM_FLAGS_ DONTCACHEMAPPINGSCHEMA 16 = STREAM_FLAGS_DONTCACHETEMPLATE 32 = STREAM_FLAGS_DONTCACHEXSL<br /><br /> En la siguiente tabla se proporciona información adicional acerca de estos valores.|  
|xml root||Esta propiedad se usa para definir una etiqueta raíz para el código XML resultante. Por ejemplo, si ejecuta consultas SQL en la base de datos y el documento XML resultante no tiene un único elemento raíz, el valor de la propiedad se usa para agregar un elemento raíz único al documento.<br /><br /> Para obtener un ejemplo en el que se utiliza esta propiedad, vea [Executing SQL Queries &#40;proveedor SQLXMLOLEDB&#41;](executing-sql-queries-sqlxmloledb-provider.md).|  
|xsl||Esta propiedad se usa para especificar el nombre del archivo XSL cuando se desea aplicar una transformación XSL al documento XML devuelto por la consulta.<br /><br /> La ruta de acceso especificada puede ser relativa (xyz/abc/MyXSL.xsl) o absoluta (C:\miCarpeta\abc\MyXSL.xsl).<br /><br /> Si se especifica una ruta de acceso relativa, se utiliza la ruta de acceso base especificada por la propiedad de ruta de acceso Base para resolver la ruta de acceso relativa. Si no se ha especificado ninguna ruta de acceso en la propiedad de ruta de acceso Base, la ruta de acceso relativa es relativa al directorio actual.<br /><br /> Para obtener un ejemplo en el que se utiliza esta propiedad, consulte aplicar una transformación XSL (proveedor SQLXMLOLEDB).|  
  
 En la tabla siguiente contiene descripciones de los valores de propiedad de las marcas de Stream ss.  
  
|Valor de propiedad|Descripción|  
|--------------------|-----------------|  
|STREAM_FLAGS_DISALLOW_URL|No se aceptan direcciones URL en esquemas de asignación o XSL.|  
|STREAM_FLAGS_DISALLOW_ABSOLTE_PATH|Una ruta de acceso especificada para un esquema de asignación o para XSL debe ser relativa a la ruta de acceso base de la propia plantilla.|  
|STREAM_FLAGS_DISALLOW_QUERY|No se permiten consultas en una plantilla.|  
|STREAM_FLAGS_DONTCACHEMAPPINGSCHEMA|El esquema de asignación no se almacena en la memoria caché. Este valor de propiedad resulta útil durante la fase de desarrollo de la base de datos, cuando los esquemas de la base de datos están sujetos a modificaciones.|  
|STREAM_FLAGS_DONTCACHETEMPLATE|Las plantillas no se almacenan en la memoria caché.|  
|STREAM_FLAGS_DONTCACHEXSL|XSL no se almacena en la memoria caché.|  
  
  

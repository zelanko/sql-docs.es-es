---
title: Compatibilidad con tipos de datos XML en SQLXML 4,0 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, xml data type support
- xml data type [SQL Server], SQLXML
ms.assetid: 9a6f5ad8-4a8f-4de7-ac17-81d5ccf78459
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0288e88e10433a3c74487b1fd1418b14a58094b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66012167"
---
# <a name="xml-data-type-support-in-sqlxml-40"></a>Compatibilidad con tipos de datos xml en SQLXML 4.0
  A partir [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , admite datos con tipo XML mediante `xml` el tipo de datos. En este tema se proporciona información sobre la forma en que SQLXML 4.0 reconoce instancias del tipo de datos `xml` y la forma en que implementa la compatibilidad con estas instancias.  
  
## <a name="working-with-xml-data-types"></a>Trabajar con tipos de datos xml  
 Para entender mejor la forma de trabajar con tablas SQL que implementan columnas de tipo de datos `xml`, se proporcionan los ejemplos siguientes:  
  
|Tarea|Ejemplo|Tema|  
|----------|-------------|-----------|  
|Cómo asignar e incluir una columna `xml` en una vista XML|"Asignar un elemento XML a una columna de tipo de datos XML"|[Asignación predeterminada de elementos y atributos XSD a tablas y columnas &#40;SQLXML 4,0&#41;](../sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)|  
|Cómo insertar datos en una columna `xml` con diagramas de actualización|"Insertar datos en una columna de tipo de datos XML"|[Insertar datos mediante XML diagramas &#40;SQLXML 4,0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)|  
|Realizar una carga masiva de datos XML en una columna `xml`|"Cargar datos de forma masiva en columnas de tipo de datos xml"|[Ejemplos de carga masiva XML &#40;SQLXML 4,0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)|  
  
## <a name="guidelines-and-limitations"></a>Instrucciones y limitaciones  
  
-   xsd: los>no se pueden asignar a una columna que `xml` incluya un tipo de datos. ** \<** En SQLXML, se proporciona compatibilidad para este escenario a través de la anotación `sql:overflow-field`. Otra solución es asignar un campo de tipo de datos `xml` como un elemento de `xsd:anyType`. Esta solución alternativa se muestra en el ejemplo "Asignar un elemento XML a una columna de tipo de datos XML", al que se hacía referencia en la tabla anterior.  
  
-   No se admiten consultas XPath en el contenido de las columnas de tipo de datos `xml`.  
  
-   El uso de una columna de tipo de datos `xml` en anotaciones donde no se admite o no se permite (como `sql:relationship` y `sql:key-fields`) producirá errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no serán capturados por los componentes de nivel intermedio que implementan SQLXML 4.0. Esto ocurre porque SQLXML no requiere información de tipos SQL. Es similar al comportamiento de SQLXML con otros tipos de datos, como los tipos BLOB y binario.  
  
-   La asignación de columnas `xml` solo se admite en esquemas XSD. Los esquemas XDR no admiten la asignación de columnas `xml`.  
  
-   SQLXML 4.0 se basa en la compatibilidad con el análisis XML que proporciona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Una columna `xml` puede asignarse como XML con tipo o XML sin tipo. En ambos casos, SQLXML 4.0 no valida el XML de entrada.  Si el XML de entrada no es válido o no tiene un formato correcto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se lo notifica a SQLXML y propaga cualquier información de error pertinente que el servidor devuelve al usuario.  
  
-   SQLXML 4.0 se basa en la compatibilidad limitada con las DTD que se proporcionan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite una DTD interna en los datos de tipo `xml`, que puede utilizarse para proporcionar valores predeterminados y reemplazar las referencias a entidades por su contenido expandido. SQLXML pasa los datos XML "tal cual" al servidor (incluida la DTD interna). Puede convertir las DTD en documentos de esquema XML (XSD) mediante herramientas de otros fabricantes y cargar los datos con esquemas XML insertados en la base de datos.  
  
-   SQLXML 4,0 no conserva las instrucciones de procesamiento de declaraciones XML (por ejemplo,) en función del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]comportamiento de. En lugar de ello, la declaración XML se trata como una directiva del analizador XML de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y sus atributos (version, encoding y standalone) se pierden una vez que los datos se han convertido al tipo `xml`. Los datos XML se almacenan internamente como UCS-2. Las demás instrucciones de procesamiento de la instancia XML se conservan; se permiten en la columna `xml` y son compatibles con SQLXML.  
  
## <a name="see-also"></a>Consulte también  
 [Datos XML &#40;SQL Server&#41;](../xml/xml-data-sql-server.md)  
  
  

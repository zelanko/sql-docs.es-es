---
title: Compatibilidad con tipos de datos xml en SQLXML 4.0
description: Obtenga información sobre cómo SQLXML 4,0 reconoce las instancias del tipo de datos XML e implementa su compatibilidad.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, xml data type support
- xml data type [SQL Server], SQLXML
ms.assetid: 9a6f5ad8-4a8f-4de7-ac17-81d5ccf78459
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8dbebdd4908b4721ce91cd5994a6a25975ebdd42
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85665507"
---
# <a name="xml-data-type-support-in-sqlxml-40"></a>Compatibilidad con tipos de datos xml en SQLXML 4.0
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite datos con tipo XML mediante el tipo de datos **XML** . En este tema se proporciona información sobre cómo SQLXML 4,0 reconoce las instancias del tipo de datos **XML** e implementa su compatibilidad.  
  
## <a name="working-with-xml-data-types"></a>Trabajar con tipos de datos xml  
 Para obtener más información sobre cómo trabajar con tablas de SQL que implementan columnas de tipo de datos **XML** , se proporcionan los ejemplos siguientes:  
  
|Tarea|Ejemplo|Tema|  
|----------|-------------|-----------|  
|Cómo asignar e incluir una columna **XML** en una vista XML|"Asignar un elemento XML a una columna de tipo de datos XML"|[Asignación predeterminada de elementos y atributos XSD a tablas y columnas &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)|  
|Cómo insertar datos en una columna **XML** con diagramas|"Insertar datos en una columna de tipo de datos XML"|[Insertar datos mediante XML diagramas &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)|  
|Cargar datos XML de forma masiva en una columna **XML**|"Cargar datos de forma masiva en columnas de tipo de datos xml"|[Ejemplos de carga masiva XML &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)|  
  
## <a name="guidelines-and-limitations"></a>Instrucciones y limitaciones  
  
-   **\<xsd:any>** no se puede asignar a una columna que incluye un tipo de datos **XML** . La compatibilidad en SQLXML para este escenario se proporciona a través de la anotación **SQL: Overflow-Field** . Otra solución consiste en asignar un campo de tipo de datos **XML** como un elemento de **xsd: anyType**. Esta solución alternativa se muestra en el ejemplo "Asignar un elemento XML a una columna de tipo de datos XML", al que se hacía referencia en la tabla anterior.  
  
-   No se admite la consulta XPath en el contenido de las columnas de tipo de datos **XML** .  
  
-   El uso de una columna de tipo de datos **XML** en anotaciones en las que no se admite (como **SQL: Relationship** y **SQL: Key-Fields**) o que se permite producirá [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] errores que no se capturarán mediante componentes de nivel intermedio que implementan SQLXML 4,0. Esto ocurre porque SQLXML no requiere información de tipos SQL. Es similar al comportamiento de SQLXML con otros tipos de datos, como los tipos BLOB y binario.  
  
-   La asignación de columnas **XML** solo se admite en esquemas XSD. Los esquemas XDR no admiten la asignación de columnas **XML** .  
  
-   SQLXML 4.0 se basa en la compatibilidad con el análisis XML que proporciona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Una columna **XML** se puede asignar como XML con tipo o XML sin tipo. En ambos casos, SQLXML 4.0 no valida el XML de entrada.  Si el XML de entrada no es válido o no tiene un formato correcto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se lo notifica a SQLXML y propaga cualquier información de error pertinente que el servidor devuelve al usuario.  
  
-   SQLXML 4.0 se basa en la compatibilidad limitada con las DTD que se proporcionan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]permite una DTD interna en datos de tipo de datos **XML** , que se puede utilizar para proporcionar valores predeterminados y reemplazar las referencias a entidades por su contenido expandido. SQLXML pasa los datos XML "tal cual" al servidor (incluida la DTD interna). Puede convertir las DTD en documentos de esquema XML (XSD) mediante herramientas de otros fabricantes y cargar los datos con esquemas XML insertados en la base de datos.  
  
-   SQLXML 4,0 no conserva las instrucciones de procesamiento de declaraciones XML (por ejemplo,) en función del comportamiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . En su lugar, la declaración XML se trata como una directiva del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] analizador XML y sus atributos (versión, codificación y independiente) se pierden después de que los datos se conviertan al tipo de datos **XML** . Los datos XML se almacenan internamente como UCS-2. Se conservan todas las demás instrucciones de procesamiento de la instancia XML; se permiten en la columna **XML** y pueden ser compatibles con SQLXML.  
  
## <a name="see-also"></a>Consulte también  
 [Datos XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  

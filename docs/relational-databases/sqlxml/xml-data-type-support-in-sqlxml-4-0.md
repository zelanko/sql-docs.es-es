---
title: compatibilidad con tipos de datos en SQLXML 4.0 XML | Microsoft Docs
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
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c1bf535dadc1f2deecd9262fd6fdc9da13045216
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47663633"
---
# <a name="xml-data-type-support-in-sqlxml-40"></a>Compatibilidad con tipos de datos xml en SQLXML 4.0
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A partir [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es compatible con XML con tipo de datos mediante el **xml** tipo de datos. En este tema se proporciona información acerca de cómo SQLXML 4.0 reconoce instancias de la **xml** tipo de datos e implementa compatibilidad para ellos.  
  
## <a name="working-with-xml-data-types"></a>Trabajar con tipos de datos xml  
 Para más información sobre cómo trabajar con tablas SQL que implementan **xml** columnas de tipo de datos se proporcionan los ejemplos siguientes:  
  
|Tarea|Ejemplo|Tema|  
|----------|-------------|-----------|  
|Cómo asignar e incluir un **xml** columna en una vista XML|"Asignar un elemento XML a una columna de tipo de datos XML"|[Asignación predeterminada de atributos y elementos XSD a tablas y columnas &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)|  
|Cómo insertar datos en un **xml** columna con los diagramas de actualización|"Insertar datos en una columna de tipo de datos XML"|[Insertar datos con diagramas de actualización XML &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)|  
|Cargar datos XML en de forma masiva un **xml** columna|"Cargar datos de forma masiva en columnas de tipo de datos xml"|[Ejemplos de carga masiva XML &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)|  
  
## <a name="guidelines-and-limitations"></a>Instrucciones y limitaciones  
  
-   **\<xsd: cualquier >** no puede asignarse a una columna que incluye un **xml** tipo de datos. Compatibilidad de SQLXML para este escenario se proporciona a través de la **Overflow-campo** anotación. Otra solución alternativa consiste en asignar una **xml** campo de tipo de datos como un elemento de **xsd: anyType**. Esta solución alternativa se muestra en el ejemplo "Asignar un elemento XML a una columna de tipo de datos XML", al que se hacía referencia en la tabla anterior.  
  
-   Consulta XPath en el contenido de **xml** columnas de tipo de datos no se admite.  
  
-   Mediante un **xml** columna de tipo de datos en las anotaciones donde no se admite (como **SQL: Relationship** y **SQL: Key-campos**) o producirá permitido en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] errores que no serán capturados por los componentes de nivel intermedio que implementan SQLXML 4.0. Esto ocurre porque SQLXML no requiere información de tipos SQL. Es similar al comportamiento de SQLXML con otros tipos de datos, como los tipos BLOB y binario.  
  
-   Asignación **xml** columnas solo se admite para los esquemas XSD. Los esquemas XDR no admiten la asignación **xml** columnas.  
  
-   SQLXML 4.0 se basa en la compatibilidad con el análisis XML que proporciona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un **xml** columna puede asignarse como XML con tipo o XML sin tipo. En ambos casos, SQLXML 4.0 no valida el XML de entrada.  Si el XML de entrada no es válido o no tiene un formato correcto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se lo notifica a SQLXML y propaga cualquier información de error pertinente que el servidor devuelve al usuario.  
  
-   SQLXML 4.0 se basa en la compatibilidad limitada con las DTD que se proporcionan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite una DTD interna en **xml** datos, lo que pueden utilizarse para proporcionar valores predeterminados y reemplazar las referencias a entidades por su contenido expandido del tipo de datos. SQLXML pasa los datos XML "tal cual" al servidor (incluida la DTD interna). Puede convertir las DTD en documentos de esquema XML (XSD) mediante herramientas de otros fabricantes y cargar los datos con esquemas XML insertados en la base de datos.  
  
-   SQLXML 4.0 no conserva instrucciones de procesamiento de declaración XML (por ejemplo), en función del comportamiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En su lugar, la declaración XML se trata como una directiva para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] analizador XML y sus atributos (versión, encoding y standalone) se pierden cuando los datos se convierten a la **xml** tipo de datos. Los datos XML se almacenan internamente como UCS-2. Se conservan todas las demás instrucciones de procesamiento en la instancia XML; se permiten en el **xml** columna y pueden ser compatibles con SQLXML.  
  
## <a name="see-also"></a>Vea también  
 [Datos XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  

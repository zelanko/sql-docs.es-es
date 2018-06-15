---
title: SQLXML 4.0 conceptos de programación | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLXML, about SQLXML
- SQLXML
ms.assetid: 5a11cda2-b8a3-4453-848f-641afdaa7024
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0071c9f56d118c3d80a92d556c29b813a25cdee1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32970510"
---
# <a name="sqlxml-40-programming-concepts"></a>Conceptos de programación en SQLXML 4.0
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  SQLXML 3.0 se proporcionó como una versión web para facilitar funcionalidad XML adicional del lado cliente y mejoras en las características existentes, como esquemas XSD anotados, carga masiva XML, compatibilidad con los servicios web (SOAP) y diagramas de actualización.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introdujo SQLXML 4.0, que continúa entregando la misma funcionalidad que SQLXML 3.0 además de actualizaciones adicionales proporcionadas para alojar las nuevas características introducidas con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 En esta sección se proporciona información sobre SQLXML 4.0.  
  
 [SQLXML no está instalado en SQL Server](../../relational-databases/sqlxml/sqlxml-is-not-installed-in-sql-server.md)  
 Describe cómo instalar SQLXML 4.0.  
  
 [Novedades de SQLXML 4.0 SP1](../../relational-databases/sqlxml/what-s-new-in-sqlxml-4-0-sp1.md)  
 Describe las actualizaciones y mejoras en SQLXML 4.0 y proporciona vínculos a los correspondientes temas de esta documentación.  
  
 [Utilizar ADO para ejecutar consultas SQLXML 4.0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)  
 Describe cómo utilizar ADO para las consultas SQLXML. ADO tiene más importancia en SQLXML 4.0 que en las versiones anteriores.  
  
 [Compatibilidad con tipos de datos xml en SQLXML 4.0](../../relational-databases/sqlxml/xml-data-type-support-in-sqlxml-4-0.md)  
 Describe la compatibilidad del tipo de datos xml agregado con SQLXML 4.0.  
  
 [Requisitos para ejecutar los ejemplos de SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)  
 Describe los requisitos para crear ejemplos funcionales a partir de los ejemplos de SQLXML proporcionados.  
  
 [Formato de cliente y servidor &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml/formatting/client-side-and-server-side-formatting-sqlxml-4-0.md)  
 Proporciona información y comparaciones de formato en el cliente y en el servidor, incluido el comando FOR XML para construir los documentos XML.  
  
 [Esquemas XSD anotados en SQLXML 4.0](../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xsd-schemas-in-sqlxml-4-0.md)  
 Proporciona información sobre cómo utilizar los esquemas XSD anotados en SQLXML 4.0. También proporciona información sobre los esquemas XDR anotados para su uso en las aplicaciones heredadas.  
  
 [Utilizar consultas XPath en SQLXML 4.0](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/using-xpath-queries-in-sqlxml-4-0.md)  
 Describe cómo usar un subconjunto del lenguaje XPath para consultar las vistas XML creadas por un esquema XSD anotado y proporciona ejemplos.  
  
 [Usar diagramas de actualización para modificar datos en SQLXML 4.0](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/using-updategrams-to-modify-data-in-sqlxml-4-0.md)  
 Proporciona información sobre los diagramas de actualización, que modifican los datos de una base de datos trabajando con las vistas XML proporcionadas por los esquemas XSD (o XDR) anotados.  
  
 [Realizar la carga masiva de datos XML & #40; SQLXML 4.0 & #41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)  
 Describe cómo hacer una carga masiva de XML en SQLXML 4.0.  
  
 [SQLXML 4.0 Data Access Components](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/sqlxml-4-0-data-access-components-sqlxmloledb-provider.md)  
 Documenta el proveedor de SQLXMLOLEDB y proporciona vínculos a otros componentes de acceso a datos de SQLXML 4.0.  
  
 [Compatibilidad SQLXML 4.0 con .NET Framework](http://msdn.microsoft.com/library/c18cf801-f893-4fbc-8e2b-c563f6108acf)  
 Describe la compatibilidad de SQLXML 4.0 con .NET Framework.  
  
 [Almacenamiento en caché de plantillas, XSL y esquemas &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/caching-templates-xsl-and-schemas-sqlxml-4-0.md)  
 Describe la funcionalidad de almacenamiento en caché proporcionada en SQLXML para mejorar el rendimiento.  
  
 [Consideraciones de seguridad de SQLXML 4.0](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/sqlxml-4-0-security-considerations.md)  
 Describe los problemas de seguridad relativos a SQLXML 4.0.  
  
 [Instrucciones y limitaciones de SQLXML 4.0](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/guidelines-and-limitations-of-sqlxml-4-0.md)  
 Enumera los problemas que se deben recordar al trabajar con SQLXML 4.0.  
  
## <a name="see-also"></a>Vea también  
 [Datos XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  

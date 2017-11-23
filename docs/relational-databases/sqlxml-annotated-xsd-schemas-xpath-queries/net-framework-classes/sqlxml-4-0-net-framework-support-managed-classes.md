---
title: Clases administradas de SQLXML | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- .NET Framework [SQLXML], Managed Classes
- SQL Server .NET Data Provider
- Managed Classes [SQLXML], about managed classes
- providers [SQLXML], SQL Server .NET Data Provider
- data providers [SQLXML], SQL Server .NET Data Provider
- Managed Classes [SQLXML]
- XML [SQLXML]
- SQLXML Managed Classes
- providers [SQLXML], SQLXML Managed Classes
- data providers [SQLXML], SQLXML Managed Classes
- SQLXML, Managed Classes
ms.assetid: 73a5faeb-dabf-4895-acb5-a9651b646065
caps.latest.revision: "25"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0f2d79aae0c863030a478ed2e3859785d491be61
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sqlxml-40-net-framework-support---managed-classes"></a>Compatibilidad SQLXML 4.0 con .NET Framework: las clases administradas
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)][!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 admite características que permiten escribir aplicaciones para tener acceso a datos XML de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], introducir los datos en el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] entorno de .NET Framework, procesen los datos y devolver las actualizaciones a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. 
  
  Las clases administradas de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML exponen la funcionalidad de SQLXML 4.0 dentro de [!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework. Con las clases administradas de SQLXML, puede escribir una aplicación C# para tener acceso a los datos XML desde una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], introducir los datos en el entorno .NET Framework, procesar los datos y devolver las actualizaciones a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como un DiffGram para aplicar las actualizaciones. Debe utilizar un esquema de asignación al aplicar actualizaciones a una base de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizando clases administradas de SQLXML. Para obtener un ejemplo funcional, vea [obtiene acceso a la funcionalidad de SQLXML en el entorno .NET](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md).  
  
 Para utilizar las clases administradas de SQLXML con SQLXML 4.0, debe instalar Microsoft Visual Studio.  
  
> [!NOTE]  
>  .NET Framework incluye el proveedor de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].NET. Este proveedor se puede utilizar para tener acceso a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] desde el entorno .NET; sin embargo, solamente puede administrar consultas SQL tradicionales (es decir, consultas a la base de datos relacional con la excepción de consultas FOR XML). No puede ejecutar plantillas XML o consultas XPath del servidor en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  

 Para obtener información sobre el acceso y modificar datos en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dentro de la [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework y sobre cómo usar DiffGrams para actualizar datos en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tablas, vea [obtiene acceso a la funcionalidad de SQLXML en el entorno de .NET](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md).  
  
> [!NOTE]  
>  También puede escribir aplicaciones de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio para realizar una carga masiva de documentos XML mediante la carga masiva XML. Para obtener más información, vea [realizar carga masiva de datos XML &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md). Debe agregar una referencia a la DLL de carga masiva XML (Xblkld4.dll) en la aplicación. Ésta es una DLL COM para la que Visual Studio .NET crea automáticamente la biblioteca de contenedores.  
  
  Esta sección proporcionan aplicaciones de ejemplo que muestran cómo usar el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] clases administradas de SQLXML:  
 [Ejecutar consultas SQL &#40; Administradas de SQLXML clases &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)  
  [Ejecutar consultas SQL mediante el método ExecuteXMLReader](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-by-using-the-executexmlreader-method.md)  
  [Procesar XML en el lado del cliente &#40; Administradas de SQLXML clases &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/processing-xml-on-the-client-side-sqlxml-managed-classes.md)  
  [Ejecutar consultas XPath &#40; Administradas de SQLXML clases &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-xpath-queries-sqlxml-managed-classes.md)  
  [Ejecutar consultas XPath con espacios de nombres &#40; Administradas de SQLXML clases &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-xpath-queries-with-namespaces-sqlxml-managed-classes.md)  
  [Ejecutar archivos de plantilla mediante la propiedad CommandText](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-template-files-by-using-the-commandtext-property.md)  
  [Ejecutar archivos de plantilla mediante la propiedad CommandStream](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-template-files-by-using-the-commandstream-property.md)  
  [Aplicar una transformación XSL &#40; Administradas de SQLXML clases &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/applying-an-xsl-transformation-sqlxml-managed-classes.md)  
  

  
  

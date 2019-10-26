---
title: Usar el proveedor SQLXMLOLEDB (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sample applications [SQLXML]
- SQLXMLOLEDB Provider, samples
- ClientSideXML property
ms.assetid: fbcefac5-29c9-478b-b0e0-d510b593f446
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9bc5e79f52f3aabbe157065db86e8d0968537ef7
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909354"
---
# <a name="using-the-sqlxmloledb-provider-sqlxml-40"></a>Usar el proveedor SQLXMLOLEDB (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En los temas de esta sección se proporcionan aplicaciones de ejemplo ADO que muestran el uso de las propiedades específicas del proveedor SQLXMLOLEDB.  
  
## <a name="application-requirements-for-sqlxmloledb-40-provider"></a>Requisitos de aplicación del proveedor de SQLXMLOLEDB 4.0  
 Para crear ejemplos funcionales que utilicen SQLXMLOLEDB 4.0, siga este procedimiento:  
  
1.  Cree una aplicación .exe en Microsoft Visual Basic y agregue una de las referencias siguientes:  
  
    -   Biblioteca de Microsoft Objetos de datos ActiveX 2,6  
  
    -   Biblioteca de Microsoft Objetos de datos ActiveX 2,7  
  
    -   Biblioteca Microsoft ActiveX Data Objects 2.8  
  
2.  Implemente e instale SQLXML 4.0 y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client  

     Para obtener más información, vea en [SQLXML 4,0 Programming Concepts](../../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md) and [Installing SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md).  
  
## <a name="in-this-section"></a>En esta sección  
 [Ejecutar consultas &#40;SQL (proveedor SQLXMLOLEDB)&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-sql-queries-sqlxmloledb-provider.md)  
 Muestra el uso de las propiedades raíz Clientsidexml, y XML para ejecutar consultas SQL.  
  
 [Ejecutar plantillas que contienen consultas &#40;SQL (proveedor SQLXMLOLEDB)&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-templates-that-contain-sql-queries-sqlxmloledb-provider.md)  
 Muestra el uso de la propiedad Clientsidexml,.  
  
 [Ejecutar consultas &#40;XPath (proveedor SQLXMLOLEDB)&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-sqlxmloledb-provider.md)  
 Muestra el uso de las propiedades Clientsidexml,, ruta de acceso base y esquema de asignación.  
  
 [Ejecutar consultas XPath con el proveedor de &#40;espacios de nombres SQLXMLOLEDB&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-with-namespaces-sqlxmloledb-provider.md)  
 Muestra cómo realizar consultas contra esquemas certificados por espacio de nombres.  
  
 [Ejecutar plantillas que contienen consultas &#40;XPath (proveedor SQLXMLOLEDB)&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-templates-that-contain-xpath-queries-sqlxmloledb-provider.md)  
 Muestra cómo ejecutar plantillas con consultas SQL mediante las propiedades Clientsidexml,, ruta de acceso base y esquema de asignación.  
  
 [Aplicar un proveedor SQLXMLOLEDB &#40;de transformación XSL&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/applying-an-xsl-transformation-sqlxmloledb-provider.md)  
 Muestra el uso de las propiedades Clientsidexml, y XSL para aplicar una transformación XSL.  
  
## <a name="see-also"></a>Ver también  
 [Requisitos del sistema para SQL Server Native Client](../../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md)  
  
  

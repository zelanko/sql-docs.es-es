---
title: Usar el proveedor SQLXMLOLEDB (SQLXML 4.0) | Microsoft Docs
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9801f34d1128595a2a23004327379cb213e1a0c7
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034636"
---
# <a name="using-the-sqlxmloledb-provider-sqlxml-40"></a>Usar el proveedor SQLXMLOLEDB (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En los temas de esta sección se proporcionan aplicaciones de ejemplo ADO que muestran el uso de las propiedades específicas del proveedor SQLXMLOLEDB.  
  
## <a name="application-requirements-for-sqlxmloledb-40-provider"></a>Requisitos de aplicación del proveedor de SQLXMLOLEDB 4.0  
 Para crear ejemplos funcionales que utilicen SQLXMLOLEDB 4.0, siga este procedimiento:  
  
1.  Cree una aplicación .exe en Microsoft Visual Basic y agregue una de las referencias siguientes:  
  
    -   Biblioteca de Microsoft ActiveX Data Objects 2.6  
  
    -   Microsoft ActiveX Data Objects Library 2.7  
  
    -   Biblioteca Microsoft ActiveX Data Objects 2.8  
  
2.  Implemente e instale SQLXML 4.0 y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client  
  
     Para obtener más información, consulte en [conceptos de programación de SQLXML 4.0](../../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md) y [instalar SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md).  
  
## <a name="in-this-section"></a>En esta sección  
 [Ejecutar consultas SQL &#40;proveedor SQLXMLOLEDB&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-sql-queries-sqlxmloledb-provider.md)  
 Muestra el uso de las propiedades de raíz ClientSideXML y xml para ejecutar consultas SQL.  
  
 [Ejecutar plantillas que contienen consultas SQL &#40;proveedor SQLXMLOLEDB&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-templates-that-contain-sql-queries-sqlxmloledb-provider.md)  
 Muestra el uso de la clientsidexml, propiedad.  
  
 [Ejecutar consultas XPath &#40;proveedor SQLXMLOLEDB&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-sqlxmloledb-provider.md)  
 Muestra el uso de las propiedades ClientSideXML, ruta de acceso Base y esquema de asignación.  
  
 [Ejecutar consultas XPath con espacios de nombres &#40;proveedor SQLXMLOLEDB&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-with-namespaces-sqlxmloledb-provider.md)  
 Muestra cómo realizar consultas contra esquemas certificados por espacio de nombres.  
  
 [Ejecutar plantillas que contienen consultas XPath &#40;proveedor SQLXMLOLEDB&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-templates-that-contain-xpath-queries-sqlxmloledb-provider.md)  
 Se muestra cómo ejecutar plantillas con consultas SQL con las propiedades ClientSideXML, ruta de acceso Base y esquema de asignación.  
  
 [Aplicar una transformación XSL &#40;proveedor SQLXMLOLEDB&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/applying-an-xsl-transformation-sqlxmloledb-provider.md)  
 Muestra el uso de las propiedades ClientSideXML y xsl en aplicar una transformación XSL.  
  
## <a name="see-also"></a>Vea también  
 [Requisitos del sistema para SQL Server Native Client](../../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md)  
  
  

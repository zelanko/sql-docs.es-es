---
title: Plantillas de almacenamiento en caché, XSL y esquemas (SQLXML)
description: Vea información sobre el almacenamiento en caché de plantillas, XSL y esquemas en SQLXML 4,0.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, caching
- cache [SQLXML]
- memory [SQLXML]
ms.assetid: 80b4fa79-243f-442c-9f22-74ad66186501
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a1481a45c65f2c6876c6acbc35d42d1706776b49
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85650495"
---
# <a name="caching-templates-xsl-and-schemas-sqlxml-40"></a>Almacenar en memoria caché plantillas, XSL y esquemas (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Para mejorar el rendimiento, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 permite almacenar en la memoria caché plantillas, archivos XSL y esquemas.  
  
 Todos los esquemas, plantillas y archivos XSL (excepto los archivos de una ubicación https://o ftp://) se almacenan en caché. Los archivos almacenados en la memoria caché permanecen en memoria mientras el proceso se está ejecutando. Cuando finaliza el proceso, se pierde toda la caché. Por consiguiente, si ejecuta un proceso por consulta, es posible que no se aprecien las ventajas del almacenamiento en caché.  
  
 Los temas de esta sección proporcionan más información sobre cómo almacenar en memoria caché.  
  
## <a name="in-this-section"></a>En esta sección  
 [Almacenamiento en caché de plantillas &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)  
 Se describe y proporciona una clave del Registro para el almacenamiento en caché de las plantillas.  
  
 [Almacenamiento en caché XSL &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
 Se describe y proporciona una clave del Registro para el almacenamiento en caché de archivos XSL.  
  
 [Almacenamiento en caché de esquemas &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)  
 Se explican cuestiones de instalación simultánea de SQLXML relacionadas con el almacenamiento en la memoria caché de esquemas y proporciona las claves del Registro para el almacenamiento en caché de esquemas.  
  
  

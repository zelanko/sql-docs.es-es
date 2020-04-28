---
title: Consideraciones de seguridad de esquemas anotadas (SQLXML)
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping schema [SQLXML], security
- annotated XDR schemas, security
- XDR schemas [SQLXML], security
- annotations [SQLXML]
- annotated XSD schemas, security
- SQLXML, annotated XSD schemas
- SQLXML, annotated XDR schemas
- security [SQLXML], annotated schemas
- XSD schemas [SQLXML], security
ms.assetid: 7d7e44dc-b6d3-4e0f-95c7-8f99930c94f2
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 87af92866658e2fa5b4f8648e2a22dbf3d1cb13f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "75252508"
---
# <a name="annotated-schema-security-considerations-sqlxml-40"></a>Consideraciones de seguridad de esquemas anotados (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A continuación figuran las instrucciones de seguridad para utilizar esquemas anotados:  
  
-   Evite el uso de asignaciones predeterminadas en los esquemas de asignación. La asignación predeterminada expone la información de la base de datos (nombres de tabla y columnas) en el documento XML resultante ya que, de forma predeterminada, los nombres de elementos se asignan a los nombres de tabla y los nombres de atributo se asignan a las nombres de columna. Por lo tanto, cualquier usuario que vea el documento XML tendrá acceso a la información de tablas y columnas de la base de datos, lo que supone un riesgo de seguridad potencial. Para evitar este riesgo, especifique nombres de elementos y atributos arbitrarios en el esquema y use anotaciones para asignarlos explícitamente a las tablas y columnas. Para obtener más información acerca del uso de la asignación predeterminada al crear esquemas XSD, vea [asignación predeterminada de elementos y atributos XSD a tablas y columnas &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md).  
  
-   Cuando se especifica una asignación explícita utilizando anotaciones, la información de bases de datos (como nombres de tablas y columnas) queda expuesta. Por consiguiente, seguramente no quiera que estos esquemas estén disponibles de forma pública.  
  
-   Ciertas consultas, como las especificadas en el esquema de asignación con recursividad (especificadas mediante anotación **Max-Depth** establecida en un valor superior), pueden tardar más tiempo en ejecutarse. Opcionalmente, puede especificar un límite de tiempo de espera estableciendo la propiedad tiempo de espera del comando (en segundos). Por ejemplo:  
  
    ```  
    cn.Open "Provider=SQLOLEDB;Server=localhost;Database=tempdb;Integrated Security=SSPI;Command Properties='Command Time Out=50';"  
    ```  
  
## <a name="see-also"></a>Consulte también  
 [Esquemas XSD anotados en SQLXML 4.0](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xsd-schemas-in-sqlxml-4-0.md)  
  
  

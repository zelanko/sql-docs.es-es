---
title: Usar ADO con ADO MD | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: ADO, using with ADO MD
ms.assetid: cfae435e-2ac3-4312-8c1e-9ca4a74cd875
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e6fde39095f4c1b68393711f2b5ca9c188cf01de
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="using-ado-with-ado-md"></a>Usar ADO con ADO MD
ADO y ADO MD son modelos de objetos relacionados pero independientes. ADO proporciona objetos para conectarse a orígenes de datos, ejecutar comandos, recuperar datos tabulares y metadatos de esquema en formato tabular y ver la información de error de proveedor. ADO MD proporciona objetos para recuperar datos multidimensionales y ver metadatos de esquema multidimensional.  
  
 Cuando se trabaja con un MDP, puede elegir usar ADO, ADO MD o ambos con su aplicación. Si hace referencia a las dos bibliotecas dentro de su proyecto, tendrá acceso completo a la funcionalidad proporcionada por su MDP.  
  
 Resulta útil en muchas ocasiones para los consumidores puedan obtener una vista tabular plana de un conjunto de datos multidimensional. Puede hacerlo mediante el uso de la propiedad ADO [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. Especificar el origen para su [conjunto de celdas](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) como el ***origen*** parámetro para el [abiertos](../../../ado/reference/ado-api/open-method-ado-recordset.md) método de un **conjunto de registros**, en lugar de como el origen de un ADO MD **Cellset**.  
  
 También puede ser útil ver los metadatos de esquema en una vista tabular en lugar de como una jerarquía de objetos. La propiedad ADO [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) método en el [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto permite al usuario abrir un **Recordset** que contiene información de esquema. El ***QueryType*** parámetro de la **OpenSchema** método tiene varias [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) valores que se refieren específicamente a los proveedores de datos multidimensionales. Estos valores son los siguientes:  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adSchemaMeasures**  
  
-   **adSchemaMembers**  
  
 Para utilizar valores de enumeración de ADO con métodos o propiedades de ADO MD, el proyecto debe hacer referencia a bibliotecas de ADO y ADO MD. Por ejemplo, puede usar la propiedad ADO **adState** valores de enumeración con ADO MD [estado](../../../ado/reference/ado-md-api/state-property-ado-md.md) propiedad. Para obtener más información acerca de cómo establecer referencias a bibliotecas, consulte la documentación de su herramienta de desarrollo.  
  
 Para obtener más información acerca de los objetos ADO y métodos, consulte el [referencia de la API de ADO](../../../ado/reference/ado-api/ado-api-reference.md).  
  
## <a name="see-also"></a>Vea también  
 [Modelo de objetos de ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (Multidimensional) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Información general de esquemas y datos multidimensionales](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programar con ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Trabajo con datos multidimensionales](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)

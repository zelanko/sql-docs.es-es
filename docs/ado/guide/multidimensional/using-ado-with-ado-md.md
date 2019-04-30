---
title: Usar ADO con ADO MD | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, using with ADO MD
ms.assetid: cfae435e-2ac3-4312-8c1e-9ca4a74cd875
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 69707e5026497a1f98ab168d71b4e6b286520fbe
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63194901"
---
# <a name="using-ado-with-ado-md"></a>Uso de ADO con ADO MD
ADO y ADO MD son modelos de objetos independientes pero relacionadas. ADO proporciona objetos para conectarse a orígenes de datos, ejecutar comandos, recuperar datos tabulares y metadatos de esquema en formato tabular y ver la información de error de proveedor. ADO MD proporciona objetos para recuperar datos multidimensionales y ver los metadatos de esquema multidimensional.  
  
 Cuando se trabaja con un MDP, puede elegir usar ADO, ADO MD o ambos con su aplicación. Haciendo referencia a las dos bibliotecas dentro de su proyecto, tendrá acceso completo a la funcionalidad proporcionada por su MDP.  
  
 Es útil con frecuencia para los usuarios obtener una vista de tabla de un conjunto de datos multidimensional. Puede hacerlo mediante el uso de la propiedad ADO [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. Especificar el origen de su [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) como el ***origen*** parámetro para el [abierto](../../../ado/reference/ado-api/open-method-ado-recordset.md) método de un **Recordset**, en lugar de como el origen de un ADO MD **Cellset**.  
  
 También puede ser útil ver los metadatos de esquema en una vista tabular en lugar de como una jerarquía de objetos. ADO [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) método en el [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto permite al usuario abrir un **Recordset** que contiene información de esquema. El ***QueryType*** parámetro de la **OpenSchema** método tiene varios [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) valores que se refieren específicamente a los proveedores de datos multidimensionales. Estos valores son los siguientes:  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adSchemaMeasures**  
  
-   **adSchemaMembers**  
  
 Para usar los valores de enumeración de ADO con ADO MD propiedades o métodos, el proyecto debe hacer referencia a bibliotecas de ADO y ADO MD. Por ejemplo, puede utilizar ADO **adState** valores de enumeración con el ADO MD [estado](../../../ado/reference/ado-md-api/state-property-ado-md.md) propiedad. Para obtener más información acerca de cómo establecer referencias a bibliotecas, consulte la documentación de la herramienta de desarrollo.  
  
 Para obtener más información sobre los métodos y objetos ADO, vea el [referencia de API de ADO](../../../ado/reference/ado-api/ado-api-reference.md).  
  
## <a name="see-also"></a>Vea también  
 [Modelo de objetos ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (Multidimensional) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Información general de esquemas y datos multidimensionales](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programar con ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Trabajo con datos multidimensionales](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)

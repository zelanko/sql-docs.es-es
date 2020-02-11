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
ms.openlocfilehash: d3c634ec056d42e97dcbea3422a0e19a33596d54
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923145"
---
# <a name="using-ado-with-ado-md"></a>Uso de ADO con ADO MD
ADO y ADO MD están relacionados pero modelos de objetos independientes. ADO proporciona objetos para conectarse a orígenes de datos, ejecutar comandos, recuperar datos tabulares y metadatos de esquema en un formato tabular, y ver la información de error del proveedor. ADO MD proporciona objetos para recuperar datos multidimensionales y ver metadatos de esquema multidimensionales.  
  
 Cuando trabaja con un MDP, puede elegir usar ADO, ADO MD o ambos con su aplicación. Al hacer referencia a ambas bibliotecas dentro del proyecto, tendrá acceso completo a la funcionalidad proporcionada por el MDP.  
  
 A menudo, resulta útil para los consumidores obtener una vista plana y tabular de un conjunto de información multidimensional. Puede hacerlo mediante el objeto de conjunto de [registros](../../../ado/reference/ado-api/recordset-object-ado.md) de ADO. Especifique el origen del conjunto de [celdas](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) como parámetro de ***origen*** para el método [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) de un conjunto de registros, en lugar de como el origen de un **conjunto**de **celdas**ADO MD.  
  
 También puede ser útil ver los metadatos del esquema en una vista tabular en lugar de como una jerarquía de objetos. El método [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) de ADO en el objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) permite al usuario abrir un **conjunto de registros** que contiene información del esquema. El parámetro ***QueryType*** del método **OpenSchema** tiene varios valores [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) que se relacionan específicamente con MDPS. Estos valores son los siguientes:  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adSchemaMeasures**  
  
-   **adSchemaMembers**  
  
 Para usar valores de enumeración de ADO con ADO MD propiedades o métodos, el proyecto debe hacer referencia a las bibliotecas de ADO y ADO MD. Por ejemplo, puede usar los valores de enumeración de ADO **adState** con la propiedad ADO MD [State](../../../ado/reference/ado-md-api/state-property-ado-md.md) . Para obtener más información acerca de cómo establecer referencias a bibliotecas, consulte la documentación de la herramienta de desarrollo.  
  
 Para obtener más información sobre los objetos y métodos de ADO, vea la referencia de la [API de ADO](../../../ado/reference/ado-api/ado-api-reference.md).  
  
## <a name="see-also"></a>Consulte también  
 [Modelo de objetos de ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (multidimensional) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Información general de los esquemas y datos multidimensionales](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programar con ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Trabajo con datos multidimensionales](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)

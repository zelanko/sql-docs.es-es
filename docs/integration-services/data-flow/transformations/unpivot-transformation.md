---
title: "Transformación Anulación de dinamización | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.unpivottrans.f1
helpviewer_keywords:
- Unpivot transformation
- more normalized data set [Integration Services]
- normalized data [Integration Services]
- datasets [Integration Services], normalized data
ms.assetid: f635c64b-a9c5-4f11-9c40-9cd9d5298c5d
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d491bb19b4eb86bd0fe75a7b8ca8e7b6e5d226b5
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="unpivot-transformation"></a>Anulación de dinamización, transformación
  La transformación Anulación de dinamización transforma un conjunto de datos sin normalizar en una versión más normalizada ampliando los valores de varias columnas de un solo registro en varios registros con los mismos valores en una sola columna. Por ejemplo, un conjunto de datos que enumera nombres de clientes tiene una fila para cada cliente, con los productos y la cantidad comprada en columnas dentro de la fila. Después de que la transformación Anulación de dinamización normaliza el conjunto de datos, el conjunto de datos contiene una fila diferente para cada producto que compró el cliente.  
  
 El diagrama siguiente muestra un conjunto de datos antes de que se anule la dinamización de los datos en la columna Product.  
  
 ![Conjunto de datos después de que se anule la dinamización](../../../integration-services/data-flow/transformations/media/mw-dts-18.gif "conjunto de datos después de que se anule la dinamización")  
  
 El diagrama siguiente muestra un conjunto de datos después de que se haya anulado la dinamización de los datos en la columna Product.  
  
 ![Conjunto de datos antes de que se anule la dinamización](../../../integration-services/data-flow/transformations/media/mw-dts-17.gif "conjunto de datos antes de que se anule la dinamización")  
  
 En algunas circunstancias, los resultados de anulación de dinamización pueden contener filas con valores no esperados. Por ejemplo, si los datos de muestra del diagrama en los que se va a anular la dinamización tuvieran valores NULL en todas las columnas Qty para Fred, el resultado incluiría solamente una fila para Fred, no cinco. La columna Qty contendría NULL o cero, dependiendo del tipo de datos de la columna.  
  
## <a name="configuration-of-the-unpivot-transformation"></a>Configuración de la transformación Anulación de dinamización  
 La transformación Anulación de dinamización incluye la propiedad personalizada **PivotKeyValue** . Esta propiedad se puede actualizar a través de una expresión de propiedad, al cargar el paquete. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Usar expresiones de propiedad en paquetes](../../../integration-services/expressions/use-property-expressions-in-packages.md) y [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Esta transformación tiene una entrada y una salida. No tiene ninguna salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información sobre las propiedades que se pueden configurar en el cuadro de diálogo **Editor de transformación Anulación de dinamización** , haga clic en uno de los siguientes temas:  
  
-   [Editor de transformación Anulación de dinamización](../../../integration-services/data-flow/transformations/unpivot-transformation-editor.md)  
  
 Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para más información sobre cómo establecer las propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
  

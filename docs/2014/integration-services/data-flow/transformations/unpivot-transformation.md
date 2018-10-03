---
title: Transformación Anulación de dinamización | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.unpivottrans.f1
helpviewer_keywords:
- Unpivot transformation
- more normalized data set [Integration Services]
- normalized data [Integration Services]
- datasets [Integration Services], normalized data
ms.assetid: f635c64b-a9c5-4f11-9c40-9cd9d5298c5d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 219f714a21175d7cdd49b58e7d7d159003af6fed
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48156875"
---
# <a name="unpivot-transformation"></a>Anulación de dinamización, transformación
  La transformación Anulación de dinamización transforma un conjunto de datos sin normalizar en una versión más normalizada ampliando los valores de varias columnas de un solo registro en varios registros con los mismos valores en una sola columna. Por ejemplo, un conjunto de datos que enumera nombres de clientes tiene una fila para cada cliente, con los productos y la cantidad comprada en columnas dentro de la fila. Después de que la transformación Anulación de dinamización normaliza el conjunto de datos, el conjunto de datos contiene una fila diferente para cada producto que compró el cliente.  
  
 El diagrama siguiente muestra un conjunto de datos antes de que se anule la dinamización de los datos en la columna Product.  
  
 ![Conjunto de datos después de que se anule la dinamización](../../media/mw-dts-18.gif "Dataset after it is unpivoted")  
  
 El diagrama siguiente muestra un conjunto de datos después de que se haya anulado la dinamización de los datos en la columna Product.  
  
 ![Conjunto de datos antes de que se anule la dinamización](../../media/mw-dts-17.gif "Dataset before it is unpivoted")  
  
 En algunas circunstancias, los resultados de anulación de dinamización pueden contener filas con valores no esperados. Por ejemplo, si los datos de muestra del diagrama en los que se va a anular la dinamización tuvieran valores NULL en todas las columnas Qty para Fred, el resultado incluiría solamente una fila para Fred, no cinco. La columna Qty contendría NULL o cero, dependiendo del tipo de datos de la columna.  
  
## <a name="configuration-of-the-unpivot-transformation"></a>Configuración de la transformación Anulación de dinamización  
 La transformación Anulación de dinamización incluye la `PivotKeyValue` propiedad personalizada. Esta propiedad se puede actualizar a través de una expresión de propiedad, al cargar el paquete. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md), [Usar expresiones de propiedad en paquetes](../../expressions/use-property-expressions-in-packages.md) y [Propiedades personalizadas de transformación](transformation-custom-properties.md).  
  
 Esta transformación tiene una entrada y una salida. No tiene ninguna salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información sobre las propiedades que se pueden configurar en el cuadro de diálogo **Editor de transformación Anulación de dinamización** , haga clic en uno de los siguientes temas:  
  
-   [Editor de transformación Anulación de dinamización](../../unpivot-transformation-editor.md)  
  
 Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](../../common-properties.md)  
  
-   [Propiedades personalizadas de transformación](transformation-custom-properties.md)  
  
 Para más información sobre cómo establecer las propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../set-the-properties-of-a-data-flow-component.md).  
  
  

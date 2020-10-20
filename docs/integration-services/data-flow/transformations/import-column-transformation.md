---
description: Transformación Importar columna
title: Transformación Importar columna | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.importcolumntrans.f1
helpviewer_keywords:
- Import Column transformation [Integration Services]
- columns [Integration Services], importing
- importing data, SSIS packages
- inserting data
ms.assetid: ac3b74c1-ef54-4297-8062-1734324fffcc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 538077633c5eb6716dc632d9635e13f92d2421b4
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194137"
---
# <a name="import-column-transformation"></a>Transformación Importar columna

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  La transformación Importar columna lee datos de archivos y agrega los datos a columnas de un flujo de datos. Un paquete puede utilizar esta transformación para agregar texto e imágenes almacenadas en archivos distintos a un flujo de datos. Por ejemplo, un flujo de datos que carga datos en una tabla que almacena información de productos puede incluir la transformación Importar columna para importar revisiones de clientes de cada producto desde archivos y agregar las revisiones al flujo de datos.  
  
 Puede configurar la transformación Importar columna de las maneras siguientes:  
  
-   Especificar las columnas a las que la transformación agrega datos.  
  
-   Especificar si la transformación debe esperar una marca de orden de bytes (BOM).  
  
    > [!NOTE]  
    >  Solo se espera una marca BOM si los datos tienen el tipo de datos DT_NTEXT.  
  
 Una columna de la entrada de la transformación contiene los nombres de los archivos en los que están almacenados los datos. Cada fila del conjunto de datos puede especificar un archivo diferente. Cuando la transformación Importar columna procesa una fila, lee el nombre del archivo, abre el archivo correspondiente en el sistema de archivos y carga su contenido en una columna de salida. El tipo de datos de la columna de salida debe ser DT_TEXT, DT_NTEXT o DT_IMAGE. Para obtener más información, vea [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 Esta transformación tiene una entrada, una salida y una salida de error.  
  
## <a name="configuration-of-the-import-column-transformation"></a>Configuración de la transformación Importar columna  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](../set-the-properties-of-a-data-flow-component.md)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para más información sobre cómo establecer las propiedades de este componente, vea [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Vea también  
 [Transformación Exportar columna](../../../integration-services/data-flow/transformations/export-column-transformation.md)   
 [Flujo de datos](../../../integration-services/data-flow/data-flow.md)   
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  

---
title: Transformación Exportar columna | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.exportcolumntrans.f1
helpviewer_keywords:
- exporting data
- append options [Integration Services]
- Export Column transformation [Integration Services]
- columns [Integration Services], exporting
- inserting data
- truncate options [Integration Services]
ms.assetid: 678d2dfc-e40c-4fbb-b2cc-42fffc44478a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ecb72ee0cb9d6e94a672f46ed523096ac4cc096e
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58379183"
---
# <a name="export-column-transformation"></a>Transformación Exportar columna
  La transformación Exportar columna lee datos de un flujo de datos e inserta dichos datos en un archivo. Por ejemplo, si el flujo de datos contiene información de productos, como una foto de cada producto, puede usar la transformación Exportar columna para guardar las imágenes en archivos.  
  
## <a name="append-and-truncate-options"></a>Opciones de anexar y truncar  
 En la tabla siguiente se describe cómo afectan a los resultados las opciones para anexar y truncar.  
  
|Anexar|Truncamiento|El archivo existe|Resultado|  
|------------|--------------|-----------------|-------------|  
|False|False|No|La transformación crea un archivo nuevo y escribe los datos en el archivo.|  
|True|False|No|La transformación crea un archivo nuevo y escribe los datos en el archivo.|  
|False|True|No|La transformación crea un archivo nuevo y escribe los datos en el archivo.|  
|True|True|No|Se produce un error al validar la transformación en tiempo de diseño. No se permite establecer ambas propiedades en `true`.|  
|False|False|Sí|Se produce un error en tiempo de ejecución. El archivo existe, pero la transformación no puede escribir en él.|  
|False|True|Sí|La transformación elimina y vuelve a crear el archivo, y escribe los datos en el archivo.|  
|True|False|Sí|La transformación abre el archivo y escribe los datos al final del archivo.|  
|True|True|Sí|Se produce un error al validar la transformación en tiempo de diseño. No se permite establecer ambas propiedades en `true`.|  
  
## <a name="configuration-of-the-export-column-transformation"></a>Configuración de la transformación Exportar columna  
 Puede configurar la transformación Exportar columna de las maneras siguientes:  
  
-   Especificar las columnas de datos y las columnas que contienen la ruta de los archivos en los que se van a escribir los datos.  
  
-   Especificar si la operación de inserción de datos anexa o trunca archivos existentes.  
  
-   Especificar si se escribe una marca de orden de bytes (BOM) en el archivo.  
  
    > [!NOTE]  
    >  Solo se escribe una BOM cuando no se anexan los datos a un archivo existente y cuando los datos tienen el tipo de datos DT_NTEXT.  
  
 La transformación utiliza pares de columnas de entrada: Una columna contiene un nombre de archivo y la otra columna contiene datos. Cada fila del conjunto de datos puede especificar un archivo diferente. Cuando la transformación procesa una fila, los datos de dicha fila se insertan en el archivo especificado. En tiempo de ejecución, la transformación crea los archivos (si no existen) y después escribe los datos en dichos archivos. Los datos deben tener un tipo de datos DT_TEXT, DT_NTEXT o DT_IMAGE. Para obtener más información, vea [Integration Services Data Types](../integration-services-data-types.md).  
  
 Esta transformación tiene una entrada, una salida y una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para más información sobre las propiedades que puede establecer en el cuadro de diálogo **Editor de transformación Exportar columna**, vea [Editor de transformación Exportar columna &#40;página Columnas&#41;](../../export-column-transformation-editor-columns-page.md).  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](../../common-properties.md)  
  
-   [Propiedades personalizadas de transformación](transformation-custom-properties.md)  
  
 Para más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../set-the-properties-of-a-data-flow-component.md).  
  
  

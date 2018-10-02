---
title: Transformación Exportar columna | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.exportcolumntrans.f1
- sql13.dts.designer.fileextractortransformation.columns.f1
- sql13.dts.designer.fileextractortransformation.errorhandling.f1
helpviewer_keywords:
- exporting data
- append options [Integration Services]
- Export Column transformation [Integration Services]
- columns [Integration Services], exporting
- inserting data
- truncate options [Integration Services]
ms.assetid: 678d2dfc-e40c-4fbb-b2cc-42fffc44478a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 36f2797d6dd3870f352aba2fc409ec1086a0bd3e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47771613"
---
# <a name="export-column-transformation"></a>Transformación Exportar columna
  La transformación Exportar columna lee datos de un flujo de datos e inserta dichos datos en un archivo. Por ejemplo, si el flujo de datos contiene información de productos, como una foto de cada producto, puede usar la transformación Exportar columna para guardar las imágenes en archivos.  
  
## <a name="append-and-truncate-options"></a>Opciones de anexar y truncar  
 En la tabla siguiente se describe cómo afectan a los resultados las opciones para anexar y truncar.  
  
|Anexar|Truncamiento|El archivo existe|Resultado|  
|------------|--------------|-----------------|-------------|  
|False|False|no|La transformación crea un archivo nuevo y escribe los datos en el archivo.|  
|True|False|no|La transformación crea un archivo nuevo y escribe los datos en el archivo.|  
|False|True|no|La transformación crea un archivo nuevo y escribe los datos en el archivo.|  
|True|True|no|Se produce un error al validar la transformación en tiempo de diseño. No se permite establecer ambas propiedades en **true**.|  
|False|False|Sí|Se produce un error en tiempo de ejecución. El archivo existe, pero la transformación no puede escribir en él.|  
|False|True|Sí|La transformación elimina y vuelve a crear el archivo, y escribe los datos en el archivo.|  
|True|False|Sí|La transformación abre el archivo y escribe los datos al final del archivo.|  
|True|True|Sí|Se produce un error al validar la transformación en tiempo de diseño. No se permite establecer ambas propiedades en **true**.|  
  
## <a name="configuration-of-the-export-column-transformation"></a>Configuración de la transformación Exportar columna  
 Puede configurar la transformación Exportar columna de las maneras siguientes:  
  
-   Especificar las columnas de datos y las columnas que contienen la ruta de los archivos en los que se van a escribir los datos.  
  
-   Especificar si la operación de inserción de datos anexa o trunca archivos existentes.  
  
-   Especificar si se escribe una marca de orden de bytes (BOM) en el archivo.  
  
    > [!NOTE]  
    >  Solo se escribe una BOM cuando no se anexan los datos a un archivo existente y cuando los datos tienen el tipo de datos DT_NTEXT.  
  
 La transformación utiliza pares de columnas de entrada: una columna contiene un nombre de archivo y la otra contiene datos. Cada fila del conjunto de datos puede especificar un archivo diferente. Cuando la transformación procesa una fila, los datos de dicha fila se insertan en el archivo especificado. En tiempo de ejecución, la transformación crea los archivos (si no existen) y después escribe los datos en dichos archivos. Los datos deben tener un tipo de datos DT_TEXT, DT_NTEXT o DT_IMAGE. Para obtener más información, vea [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 Esta transformación tiene una entrada, una salida y una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="export-column-transformation-editor-columns-page"></a>Editor de transformación Exportar columna (página Columnas)
  Use la página **Columnas** del cuadro de diálogo **Editor de transformación Exportar columna** para especificar las columnas del flujo de datos que desea extraer a los archivos. Podrá especificar si desea que la transformación Exportar columna anexe los datos a un archivo o sobrescriba un archivo existente.  
  
### <a name="options"></a>Opciones  
 **Columna Extraer**  
 Seleccione de la lista las columnas de entrada que contengan datos de texto o imagen. Todas las filas deben poseer definiciones para la **Columna Extraer** y la **Columna Ruta de archivo**.  
  
 **Columna Ruta de archivo**  
 Seleccione de la lista las columnas de entrada que contengan rutas de archivo y nombres de archivo. Todas las filas deben poseer definiciones para la **Columna Extraer** y la **Columna Ruta de archivo**.  
  
 **Permitir la anexión**  
 Especifique si desea que la transformación anexe los datos a los archivos existentes. El valor predeterminado es **false**.  
  
 **Forzar el truncamiento**  
 Especifique si desea que la transformación elimine el contenido de los archivos existentes antes de escribir los datos. El valor predeterminado es **false**.  
  
 **BOM de escritura**  
 Especifique si desea escribir una marca de orden de bytes (BOM) en el archivo. Solo se escribirá una BOM si los datos poseen el tipo de datos **DT_NTEXT** o DT_WSTR y no están anexados a un archivo de datos existente.  
  
## <a name="export-column-transformation-editor-error-output-page"></a>Editor de transformación Exportar columna (página Salida de error)
  Use la página **Salida de error** del cuadro de diálogo **Editor de transformación Exportar columna** para especificar cómo se controlan los errores.  
  
### <a name="options"></a>Opciones  
 **Entrada/salida**  
 Muestra el nombre de la salida. Haga clic en el nombre para expandir la vista e incluir columnas.  
  
 **Columna**  
 Muestra las columnas de salida que se han seleccionado en la página **Columnas** del cuadro de diálogo **Editor de transformación Exportar columna** .  
  
 **Error**  
 Permite especificar qué debe ocurrir si se produce un error: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Truncamiento**  
 Permite especificar qué debe ocurrir si se produce un truncamiento: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Descripción**  
 Muestra la descripción de la operación.  
  
 **Establecer este valor en las celdas seleccionadas**  
 Permite especificar qué debe ocurrir en todas las celdas seleccionadas cuando se produce un error o un truncamiento: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Aplicar**  
 Aplica la opción de control de errores a las celdas seleccionadas.  
  
  

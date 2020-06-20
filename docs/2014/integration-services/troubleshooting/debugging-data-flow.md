---
title: Depurar el flujo de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- progress reporting [Integration Services]
- data viewers [Integration Services]
- data flow [Integration Services], debugging
- debugging [Integration Services], data flow
- counting rows
ms.assetid: 1c574f1b-54f7-4c05-8e42-8620e2c1df0f
author: janinezhang
ms.author: janinez
ms.openlocfilehash: cc99e29d95aa08ce9363ca1fa6971d7602824868
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972775"
---
# <a name="debugging-data-flow"></a>Depurar el flujo de datos
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] incluyen características y herramientas que puede usar para solucionar los problemas de los flujos de datos en un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] proporciona visores de datos.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] y las transformaciones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporcionan recuentos de filas.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] proporciona informes de progreso en tiempo de ejecución.  
  
## <a name="data-viewers"></a>Visores de datos  
 Los visores de datos muestran datos entre dos componentes en un flujo de datos. Los visores de datos pueden mostrar datos cuando los datos se extraen de un origen de datos y entran por primera vez en un flujo de datos, antes y después de que una transformación actualice los datos, y antes de que los datos se carguen en su destino.  
  
 Para ver los datos, se adjuntan visores de datos a la ruta que conecta dos componentes de flujo de datos. La capacidad para ver datos entre componentes de flujo de datos hace que sea más fácil identificar valores de datos inesperados, ver la forma en que una transformación cambia los valores de columna y detectar el motivo por el cual una transformación genera errores. Por ejemplo, puede ocurrir que una búsqueda en una tabla de referencia genere un error, y para corregir esto puede ser necesario agregar una transformación que proporcione datos predeterminados para columnas en blanco.  
  
 Un visor de datos puede mostrar los datos en una cuadrícula. Con una cuadrícula, se seleccionan las columnas que se muestran. Los valores de las columnas seleccionadas se muestran en formato tabular.  
  
 También puede incluir varios visores de datos en una ruta. Puede mostrar los mismos datos en distintos formatos (por ejemplo, crear una vista de gráfico y una vista de cuadrícula de los datos), o bien puede crear varios visores de datos para diferentes columnas de datos.  
  
 Cuando se agrega un visor de datos a una ruta, el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] agrega un icono de visor de datos a la superficie de diseño de la pestaña **Flujo de datos** , junto a la ruta. Las transformaciones que pueden tener varias salidas, como la transformación División condicional, pueden incluir un visor de datos en cada ruta.  
  
 En el tiempo de ejecución, se abre una ventana de **Visor de datos** , que muestra la información especificada por el formato de visor de datos. Por ejemplo, un visor de datos que usa el formato de cuadrícula muestra datos para las columnas seleccionadas, la cantidad de filas de salida que se pasan al componente de flujo de datos y la cantidad de filas que se muestran. La información muestra cada búfer individualmente y, según el ancho de las filas en el flujo de datos, un búfer puede contener más o menos filas.  
  
 En el cuadro de diálogo **Visor de datos** , puede copiar los datos en el Portapapeles, eliminar todos los datos de la tabla, reconfigurar el visor de datos, reanudar el flujo de datos y separar o adjuntar el visor de datos.  
  
#### <a name="to-add-a-data-viewer"></a>Para agregar un visor de datos  
  
-   [Agregar un visor de datos a un flujo de datos](../add-a-data-viewer-to-a-data-flow.md)  
  
## <a name="row-counts"></a>Recuentos de filas  
 La cantidad de filas que han pasado por una ruta aparece en la superficie de diseño de la pestaña **Flujo de datos** en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] junto a la ruta. La cantidad se actualiza periódicamente mientras los datos pasan por la ruta.  
  
 También puede agregar una transformación Recuento de filas al flujo de datos para capturar el recuento de filas final en una variable. Para más información, consulte [Row Count Transformation](../data-flow/transformations/row-count-transformation.md).  
  
## <a name="progress-reporting"></a>Informes de progreso  
 Al ejecutar un paquete, el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] muestra el progreso en la superficie de diseño en la pestaña **Flujo de datos** , mostrando cada componente de flujo de datos con un color que indica el estado. Cuando cada componente empieza a ejecutar su trabajo, cambia de incoloro a amarillo, y cuando termina correctamente, se cambia a verde. El color rojo indica un error del componente.  
  
 En la tabla siguiente se describen los códigos de colores.  
  
|Color|Descripción|  
|-----------|-----------------|  
|Sin color|Espera la llamada del motor de flujo de datos.|  
|Amarillo|Ejecución de una transformación, extracción de datos o carga de datos.|  
|Verde|Ejecución correcta.|  
|rojo|Ejecución con errores.|  
  
## <a name="see-also"></a>Consulte también  
 [Herramientas para solucionar problemas con el desarrollo de paquetes](troubleshooting-tools-for-package-development.md)  
  
  

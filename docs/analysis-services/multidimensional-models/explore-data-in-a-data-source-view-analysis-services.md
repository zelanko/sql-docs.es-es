---
title: Explorar datos en una vista del origen de datos (Analysis Services) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4a7cb3d9895c7524bf0517270b50ac7830774dd9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34026842"
---
# <a name="explore-data-in-a-data-source-view-analysis-services"></a>Explorar datos en una vista del origen de datos (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Puede usar el cuadro de diálogo **Explorar datos** del Diseñador de vistas del origen de datos de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para explorar los datos de una tabla, vista o consulta con nombre en una vista del origen de datos (DSV). Al explorar los datos en el Diseñador de vistas del origen de datos, puede ver el contenido de cada columna de datos de una tabla, vista o consulta con nombre seleccionada. Observar el contenido real le puede ayudar a determinar si todas las columnas son necesarias, si se necesitan cálculos con nombre para mejorar la facilidad de uso, y si los cálculos o consultas con nombre devuelven los valores previstos.  
  
 Para ver datos, debe tener una conexión activa con el origen u orígenes de datos del objeto seleccionado en la DSV. En la consulta también se envían todos los cálculos con nombre de la tabla.  
  
 Los datos se devuelven en formato tabular, y pueden ordenarse y copiarse. Haga clic en los encabezados de columna para reordenar las filas por esa columna. También puede resaltar datos en la cuadrícula y presionar Ctrl+C para copiar la selección en el portapapeles.  
  
 Asimismo, puede controlar el método de muestreo y el número de muestras. De forma predeterminada, se devuelven las 5000 principales filas.  
  
## <a name="to-browse-data-or-change-sampling-options"></a>Para examinar los datos o cambiar las opciones de muestreo  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto o conéctese a la base de datos que contiene la vista del origen de datos en que desea examinar los datos.  
  
2.  En el Explorador de soluciones, expanda la carpeta **Vistas del origen de datos** y, después, haga doble clic en la vista del origen de datos.  
  
3.  Haga clic con el botón derecho en la tabla, vista o consulta con nombre que contiene los datos que quiere ver y, después, haga clic en **Explorar datos**.  
  
     Los datos de origen subyacente de la tabla, vista o consulta con nombre de la vista del origen de datos son las consultas y los resultados aparecen en la **explorar \<nombre de objeto > tabla** ficha.  
  
4.  En el **explorar \<nombre de objeto > tabla** barra de herramientas, haga clic en el **opciones de muestreo** icono.  
  
     Se abrirá el cuadro de diálogo **Opciones de exploración de datos** . En este cuadro de diálogo puede especificar el método de muestreo (más o menos registros que el tamaño de muestreo predeterminado de 5000 filas) o el número de muestras.  
  
5.  Haga clic en **Aceptar** o en **Cancelar** , según corresponda.  
  
6.  Para volver a muestrear los datos, haga clic en **volver a muestrear datos** en el **explorar \<nombre de objeto > tabla** barra de herramientas.  
  
## <a name="see-also"></a>Vea también  
 [Vistas del origen de datos en modelos multidimensionales](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  

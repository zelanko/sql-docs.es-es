---
title: Cuadro de diálogo especificar asignación de columna (gráfico de precisión de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.coltotablecolmapping.f1
ms.assetid: 68e9e2d2-173f-4363-a515-fc60bfee3af0
author: minewiskan
ms.author: owend
ms.openlocfilehash: 625a3f2870590b77db84b3266ebf90f5081152d1
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940414"
---
# <a name="specify-column-mapping-dialog-box-mining-accuracy-chart"></a>Cuadro de diálogo Especificar asignación de columna (gráfico de precisión de minería de datos)
  Utilice la pestaña **Especificar asignación de columnas** para seleccionar las tablas de un origen de datos externo y asignar las columnas a un modelo de minería de datos. Después puede utilizar los datos externos para probar la exactitud de un modelo de minería y mostrar los resultados en el gráfico de precisión.  
  
 **Para más información:** [Prueba y validación &#40;minería de datos&#41;](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>Opciones  
 **Estructura de minería de datos**  
 Muestra la estructura de minería de datos seleccionada que contiene el modelo que probará.  
  
 **Seleccionar estructura**  
 Haga clic para abrir el cuadro de diálogo **Seleccionar estructura de minería de datos** y seleccione una estructura de minería de datos diferente.  
  
 **Seleccionar tabla(s) de entrada**  
 Muestra las tablas de entrada seleccionadas que se usan para generar el gráfico de elevación. Seleccione la tabla que contiene los datos de prueba que va a utilizar para probar la precisión de los modelos.  
  
> [!NOTE]  
>  Si el panel no contiene ninguna tabla, haga clic en **Seleccionar tabla de casos** para agregar las tablas de una vista del origen de datos.  
  
 **Quitar tabla**  
 Quita la tabla seleccionada. Este botón está deshabilitado si no se ha seleccionado una tabla o si no se muestra ninguna tabla en la lista **Seleccionar tabla(s) de entrada** .  
  
 **Seleccionar tabla de casos**  
 Haga clic para abrir el cuadro de diálogo **Seleccionar tabla** y seleccione una vista del origen de datos.  
  
 **Nota** : este botón solo aparece si no se ha seleccionado una tabla de casos. Para habilitar el botón de modo que pueda seleccionar una tabla de casos diferente, borre la lista seleccionando todas las tablas existentes y haciendo clic en **Quitar tabla**.  
  
 **Seleccionar tabla anidada**  
 Abre el cuadro de diálogo **Seleccionar tabla** . Este botón solo aparece si se ha seleccionado una tabla de casos. Este botón se deshabilita si la estructura de minería de datos asociada no contiene una tabla anidada.  
  
 **Modificar combinación**  
 Abre el cuadro de diálogo **Especificar combinación anidada** . Este botón solo está activo si se ha seleccionado una tabla anidada.  
  
## <a name="see-also"></a>Consulte también  
 [Tareas y procedimientos de prueba y validación &#40;&#41;de minería de datos](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [Diseñador de gráficos de precisión de minería de datos &#40;&#41;de minería de datos](mining-accuracy-chart-designer-data-mining.md)  
  
  

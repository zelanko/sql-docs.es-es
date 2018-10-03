---
title: Filtrar (gráfico de precisión de minería de datos) del cuadro de diálogo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 71e884a9-7ec4-4459-a4c4-87f6c796d478
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 87d3273367196d2c0c60780a3f1fa125c0b3bf8e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48060181"
---
# <a name="filter-dialog-box-mining-accuracy-chart"></a>Cuadro de diálogo Filtrar (gráfico de precisión de minería de datos)
  El cuadro de diálogo **Filtrar** ayuda a generar las condiciones que se pueden aplicar a un conjunto de datos. El conjunto de datos puede ser un conjunto de datos externo que se use para las pruebas o los datos del caso que se usen para entrenar un modelo de minería de datos. Este cuadro de diálogo ayuda a generar criterios que se pueden guardar como parte de criterios de filtro más complejos en los cuadros de diálogo **Filtro de conjunto de datos** o **Filtro del modelo** .  
  
-   El cuadro de diálogo **Filtro de conjunto de datos** está disponible en la pestaña **Selección de entrada** del diseñador **Gráfico de precisión de minería de datos** .  
  
-   El cuadro de diálogo **Filtro de modelos** está disponible en la pestaña **Modelos de minería de datos** del diseñador Minería de datos.  
  
 Si está aplicando un filtro a un modelo de minería de datos, use primero el cuadro de diálogo **Filtro del modelo** para elegir una tabla. A continuación, puede utilizar el cuadro de diálogo **Filtrar** para generar las condiciones que solo se aplican a esa tabla.  
  
 Si va a crear un filtro para aplicarlo a un conjunto de datos de pruebas externo, use primero el cuadro de diálogo **Filtro de conjunto de datos** para elegir una tabla de la lista de tablas en una vista del origen de datos. A continuación, use el cuadro de diálogo **Filtrar** para generar las condiciones que solo se aplican a esa tabla.  
  
 Cuando haya creado un conjunto de condiciones que se aplican a una única tabla, [!INCLUDE[clickOK](../includes/clickok-md.md)]. Los cambios que realizó en el cuadro de diálogo **Filtrar** se agregan automáticamente a la expresión de filtro en el cuadro de diálogo primario, **Filtro de conjunto de datos** o **Filtro del modelo**.  
  
 Si aplica el filtro al conjunto de datos nuevo, el modelo de minería de datos existente se usa para evaluar solo los casos en el conjunto de datos que cumplen las condiciones. Sin embargo, si aplica el filtro al propio modelo de minería de datos, la exactitud del modelo se evalúa solo para los casos dentro del modelo que cumplen esos criterios.  
  
 **Para más información:** [Prueba y validación &#40;minería de datos&#41;](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>Opciones  
 **Condiciones**  
 Una cuadrícula que contenga columnas en las que se especifiquen condiciones de las columnas de la tabla que se seleccionó en el cuadro de diálogo **Filtro de conjunto de datos** .  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Y/O**|Haga clic en esta opción para especificar si se aplica el operador Y o el operador O a la condición en esta línea. Estos valores solo están disponibles después de haber seleccionado una columna en la lista **Columna de la estructura de minería de datos** .|  
|**Columna de estructura de minería de datos**|Haga clic en esta opción para seleccionar una columna de la lista de columnas de la tabla que seleccionó en el origen de datos, en el cuadro de diálogo **Filtro de conjunto de datos** .|  
|**Operador**|Seleccione un operador de la lista. Los operadores que están disponibles dependen del tipo de datos de la columna.<br /><br /> Si la columna contiene valores discretos, solo están disponibles los operadores siguientes:<br /><br /> = (equal to), <> (not equal to), IS NOT NULL, IS NULL.<br /><br /> Si la columna contiene valores continuos, también se admiten los operadores correspondientes a operaciones de tipo mayor que y menor que.|  
|**Valor**|Escriba un valor que utilizar como condición.|  
  
## <a name="see-also"></a>Vea también  
 [Pruebas y validación tareas y procedimientos &#40;minería de datos&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [Diseñador gráfico de precisión de minería de datos &#40;minería de datos&#41;](mining-accuracy-chart-designer-data-mining.md)  
  
  

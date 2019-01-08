---
title: Consulta (datos de SQL Server a los complementos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- queries [data mining]
- Data Mining Query Advanced Editor
- query builder [data mining]
- DMX
ms.assetid: 16af4a6f-18d4-496a-a304-7a13aa32ee76
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b596612d711925687087a2263013fdf13a0c491e
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52418466"
---
# <a name="query-sql-server-data-mining-add-ins"></a>Consulta (Complementos de minería de datos de SQL Server)
  ![Botón de consulta de modelo, cinta de opciones minería de datos](media/dmc-query.gif "botón modelo de consultas, cinta de opciones minería de datos")  
  
 El Asistente para **Consulta** le permite interactuar con modelos de minería de datos existentes con el fin de realizar predicciones a partir de los datos de una tabla de Excel, un rango de Excel u otro origen de datos. El proceso de aplicar nuevos datos a un modelo existente para predecir tendencias se denomina *consulta de predicción*.  
  
 El asistente para **Consulta** también proporciona un editor avanzado para la creación o modificación de modelos de minería de datos, para la generación de consultas personalizadas o para trabajar con estructuras que no admiten otras herramientas, como conjuntos de datos anidados.  
  
-   Utilice el editor de texto para escribir o pegar en las instrucciones de extensiones de minería de datos (DMX) que ha creado en otro lugar.  
  
-   Use el Generador de consultas interactivo para crear una instrucción DMX personalizada con la ayuda de plantillas y cuadros de diálogo.  
  
-   Cree instrucciones DMX para administrar o para realizar copias de seguridad de modelos y estructuras de minería de datos.  
  
## <a name="using-the-query-wizard"></a>Usar el Asistente para consulta de minería de datos  
  
1.  En primer lugar, debe especificar un origen de datos para usarlo como entrada. Puede usar datos de una tabla o un rango de Excel existente, o bien especificar una instrucción SQL para recuperar los datos.  
  
2.  A continuación, el asistente muestra una lista de los modelos de minería de datos del servidor al que está conectado. Si conoce el modelo que desea usar y está familiarizado con la minería de datos, puede hacer clic también en **Avanzadas** para abrir el **Editor de consultas avanzadas de minería de datos**.  
  
3.  Dependiendo del tipo de modelo que elija, deberá especificar la columna que contenga los datos que desea evaluar y deberá definir asignaciones entre las columnas de datos de entrada y las columnas del modelo. En función del algoritmo que elija, podrá establecer otras propiedades en el modelo.  
  
4.  Por último, el asistente le ofrece también la posibilidad de elegir una o varias predicciones, y especificar un destino donde guardar los resultados.  
  
 En cualquier momento puede hacer clic en **Avanzadas** para cambiar al **Editor de consultas avanzadas de minería de datos**, que le permitirá controlar mejor cada parte de la instrucción DMX. Para obtener más información sobre cómo usar las herramientas de edición de consultas avanzadas, vea [avanzada Editor de consultas de minería de datos](advanced-data-mining-query-editor.md).  
  
### <a name="requirements"></a>Requisitos  
 Para utilizar el **Asistente para consultade minería de datos** , debe estar conectado a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Además, el servidor debe contener como mínimo un modelo de minería de datos de un tipo adecuado. Si no hay disponible ningún modelo de minería de datos, puede crear uno con los asistentes que ofrece el Cliente de minería de datos para Excel. Para obtener información sobre cómo crear un nuevo modo de minería de datos mediante un asistente, vea [crear un modelo de minería de datos](creating-a-data-mining-model.md).  
  
## <a name="see-also"></a>Vea también  
 [Implementar y ampliar modelos de minería de datos &#40;datos complementos de minería de datos para Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)   
 [Cliente de minería de datos para Excel &#40;complementos de minería de datos de SQL Server&#41;](data-mining-client-for-excel-sql-server-data-mining-add-ins.md)  
  
  

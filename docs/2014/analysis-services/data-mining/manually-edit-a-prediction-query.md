---
title: Editar manualmente una consulta de predicción | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- modifying prediction queries
- Mining Model Prediction [Analysis Services], modifying prediction queries
- manual prediction query modification [Analysis Services]
ms.assetid: 9f6a9298-49d5-4675-ad49-977a47dff5a6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ce2086e998704e893beaa92aabd2e51129a0450f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66084210"
---
# <a name="manually-edit-a-prediction-query"></a>Modificar manualmente una consulta de predicción
  Después de diseñar una consulta mediante el Generador de consultas de predicción, puede modificarla cambiando a la vista Texto de consulta en la pestaña **Predicción de modelo de minería de datos** del Diseñador de minería de datos. Un editor de texto aparece en la parte inferior de la pantalla donde se muestra la consulta creada por el generador de consultas.  
  
 Cambiar a la la vista de texto de consulta es útil para realizar adiciones a la consulta. Por ejemplo, puede agregar una cláusula WHERE o cláusula ORDER BY.  
  
 Use la cuadrícula del Generador de consultas de predicción para insertar los nombres de objetos y de columnas y configurar la sintaxis de las funciones de predicción y, a continuación cambie al modo manual para modificar los valores de parámetro.  
  
> [!NOTE]  
>  Si regresa a la vista **Diseño** desde la vista **Texto de consulta** , se perderán todos los cambios realizados en la vista **Texto de consulta** .  
  
### <a name="modify-a-query"></a>Modificar una consulta  
  
1.  En la pestaña **Predicción de modelo de minería de datos** del Diseñador de minería de datos de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga clic en **SQL**.  
  
     La cuadrícula de la parte inferior de la pantalla se sustituye por un editor de texto que contiene la consulta. En este editor puede escribir los cambios que desea realizar en la consulta.  
  
2.  Para ejecutar la consulta, en el menú **Modelo de minería de datos** , seleccione **Resultado**o haga clic en el botón para cambiar a los resultados de la consulta.  
  
    > [!NOTE]  
    >  Si la consulta que ha creado no es válida, la ventana Resultados no muestra errores ni resultados. Haga clic en el botón **Diseño** , o seleccione **Diseño** o **Consulta** en el menú **Modelo de minería de datos** para corregir el problema y ejecutar de nuevo la consulta.  
  
## <a name="see-also"></a>Consulte también  
 [Consultas de minería de datos](data-mining-queries.md)   
 [Predicción Generador de consultas &#40;de minería de datos&#41;](../prediction-query-builder-data-mining.md)   
 [Lección 6: Crear y trabajar con predicciones &#40;Tutorial básico de minería de datos&#41;](../../tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
  
  

---
title: "Editar manualmente una consulta de predicción | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying prediction queries
- Mining Model Prediction [Analysis Services], modifying prediction queries
- manual prediction query modification [Analysis Services]
ms.assetid: 9f6a9298-49d5-4675-ad49-977a47dff5a6
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 57f892500d2ef26dc2227b4c0710c4d039dcb34e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

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
  
## <a name="see-also"></a>Vea también  
 [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md)   
 [Generador de consultas de predicción &#40; minería de datos &#41;](http://msdn.microsoft.com/library/12900d49-db88-48bb-a5f4-0a9a172bc126)   
 [Lección 6: Crear y trabajar con predicciones &#40;Tutorial básico de minería de datos&#41;](http://msdn.microsoft.com/library/b213cb58-2c40-4c89-b08b-d3c36a4afad3)  
  
  


---
title: Ver y guardar los resultados de una consulta de predicción | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- prediction queries [Analysis Services]
- viewing prediction query results
- displaying prediction query results
- Mining Model Prediction [Analysis Services], viewing results
ms.assetid: abba4d24-3619-44c1-8279-88f27ad627d3
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3d7cfbd171ea3762dae468c9d418bbd9693dd6ac
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106456"
---
# <a name="view-and-save-the-results-of-a-prediction-query"></a>Ver y guardar los resultados de una consulta de predicción
  Tras definir una consulta en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mediante el Generador de consultas de predicción, puede ejecutar la consulta y ver los resultados al cambiar a la vista de resultado de consulta.  
  
 Puede guardar los resultados de una consulta de predicción en una tabla de cualquier origen de datos que esté definido en un proyecto de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Puede crear una tabla nueva o guardar los resultados de la consulta en una tabla existente. Si guarda los resultados en una tabla existente, puede elegir sobrescribir los datos que están almacenados actualmente en la tabla. En caso contrario, los resultados se anexan a los datos existentes en la tabla.  
  
### <a name="run-a-query-and-view-the-results"></a>Ejecutar una consulta y ver los resultados  
  
1.  En la barra de herramientas de la pestaña **Predicción de modelos de minería de datos** del Diseñador de minería de datos en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga clic en **Resultado** .  
  
     Se abre la vista de resultados de consulta y se ejecuta la consulta. Los resultados se muestran en una cuadrícula del visor.  
  
### <a name="save-the-results-of-a-prediction-query-to-a-table"></a>Guardar los resultados de una consulta de predicción en una tabla  
  
1.  En la barra de herramientas de la pestaña **Predicción de modelos de minería de datos** del Diseñador de minería de datos, haga clic en **Guardar resultado de consulta**.  
  
     Se abre el cuadro de diálogo **Guardar resultado de consulta de minería de datos** .  
  
2.  Seleccione un origen de datos en la lista **Origen de datos** o haga clic en **Nuevo** para crear un origen de datos nuevo.  
  
3.  En el cuadro **Nombre de la tabla** , escriba el nombre de la tabla. Si la tabla ya existe, seleccione **Sobrescribir si existe** para sustituir el contenido de la tabla con los resultados de la consulta. Si no desea sobrescribir el contenido de la tabla, no active esta casilla. Los resultados de la nueva consulta se anexan a los datos existentes en la tabla.  
  
4.  Seleccione una vista del origen de datos en **Agregar a vista del origen de datos** si desea agregar la tabla a una vista del origen de datos.  
  
5.  Haga clic en **Guardar**.  
  
    > [!WARNING]  
    >  Si el destino no admite conjuntos de filas jerárquicos, puede agregar la palabra clave FALTTENED a los resultados para guardarlos como una tabla plana.  
  
  
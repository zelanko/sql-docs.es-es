---
title: Panel de consulta (vista predicción de modelo de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.prediction.query.f1
ms.assetid: fdeec72e-d0bd-4453-9eaa-46436e4d6edc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6bfb0a0c4e8284173a102b034a8b19457340a286
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66070516"
---
# <a name="query-pane-mining-model-prediction-view"></a>Panel de consulta (Vista Predicción de modelo de minería de datos)
  En el panel **Consulta** se muestran las instrucciones DMX (Extensiones de minería de datos) creadas por el Generador de consultas de predicción. Puede modificar las instrucciones y, a continuación, hacer clic en el botón **Cambiar a vista de resultado de consulta** para devolver los resultados. Si cambia a la vista **Diseño** , se perderán los cambios realizados a la instrucción.  
  
 **Para obtener más información:** [extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](/sql/dmx/dmx-statements-data-manipulation), [crear una consulta DMX en SQL Server Management Studio](data-mining/create-a-dmx-query-in-sql-server-management-studio.md)  
  
## <a name="options"></a>Opciones  
 **Cambiar a vista de resultado de consulta**  
 Haga clic para cambiar entre los paneles **Diseño**, **Consulta**y **Resultado** . Al cambiar al panel **Resultado** se ejecuta la consulta.  
  
 **Guardar el resultado de la consulta**  
 Abre el cuadro de diálogo **Guardar resultado de consulta de minería de datos** .  
  
 **Consulta singleton**  
 Le permite crear una consulta singleton, en la que proporciona los datos de entrada directamente en la consulta en lugar de proporcionar una referencia a una tabla de valores de entrada. La tabla **Seleccionar tabla(s) de entrada** se reemplaza por una tabla **Entrada de consulta singleton** . Se perderá la consulta de predicción actual si cambia a una consulta singleton.  
  
 **Actualizar el resultado de la consulta**  
 Vuelve a procesar la consulta de predicción. Esto solo está habilitado en el panel **Resultado** .  
  
## <a name="see-also"></a>Consulte también  
 [Interfaces de consulta de minería de datos](data-mining/data-mining-query-tools.md)   
 [Referencia de instrucciones de extensiones de minería de datos &#40;DMX&#41;](/sql/dmx/data-mining-extensions-dmx-statements)   
 [Predicción Generador de consultas &#40;de minería de datos&#41;](prediction-query-builder-data-mining.md)  
  
  

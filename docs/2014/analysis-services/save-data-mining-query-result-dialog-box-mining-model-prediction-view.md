---
title: Guardar los datos de minería de datos de cuadro de diálogo resultado de consulta (vista predicción de modelo de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dm.savedataminingqueryresult.f1
helpviewer_keywords:
- Save Data Mining Query Result dialog box
ms.assetid: 112fb527-7466-4fd4-9cf1-75596135648f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b6b5c5f74ba8951bae27193b6796f09dcbdb8302
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748007"
---
# <a name="save-data-mining-query-result-dialog-box-mining-model-prediction-view"></a>Guardar resultado de consulta de minería de datos (cuadro de diálogo de la vista Predicción de modelo de minería de datos)
  Use el cuadro de diálogo **Guardar resultado de consulta de minería de datos** para guardar los resultados de una consulta de minería de datos en una tabla nueva.  
  
 La tabla nueva se creará en la base de datos que haya definido el origen de datos.  
  
## <a name="options"></a>Opciones  
 **Origen de datos**  
 Seleccione un origen de datos del proyecto actual. Si no existe el origen de datos correcto, haga clic en **Nuevo** para crear un nuevo origen de datos.  
  
 **Nueva**  
 Abre el **Asistente para orígenes de datos**.  
  
 **Nombre de tabla**  
 Escriba un nombre para la nueva tabla.  
  
 **Sobrescribir si existe**  
 Seleccione esta opción si desea sobrescribir una tabla existente con el mismo nombre.  
  
 Es preciso sobrescribir la tabla existente si se cumple alguna de las siguientes condiciones:  
  
-   Agregó columnas a la consulta de predicción.  
  
-   Cambió los nombres o los tipos de datos de cualquier columna de la consulta de predicción.  
  
-   Ejecutó una instrucción ALTER en la tabla de destino.  
  
 Si varias columnas tienen el mismo nombre (por ejemplo, es posible que varias columnas derivadas tengan el nombre de columna predeterminado **Expresión**), será preciso crear un alias para cada columna con un nombre duplicado. Si las columnas no tienen nombres únicos, se producirá un error cuando el diseñador intente guardar los resultados en SQL Server, porque las columnas de una tabla deben tener nombres únicos.  
  
 **Agregar a la DSV**  
 (Opcional) Seleccione una vista del origen de datos que contenga el proyecto si desea agregar la tabla a un origen de datos existente.  
  
 Esta opción es útil si desea conservar todas las tablas relacionadas para un modelo, como datos de entrenamiento, datos de origen de predicción y consulta los resultados de mismo origen de datos.  
  
## <a name="see-also"></a>Vea también  
 [Generador de consultas de predicción &#40;Minería de datos&#41;](prediction-query-builder-data-mining.md)   
 [Interfaces de consultas de minería de datos](data-mining/data-mining-query-tools.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](/sql/dmx/data-mining-extensions-dmx-statements)  
  
  

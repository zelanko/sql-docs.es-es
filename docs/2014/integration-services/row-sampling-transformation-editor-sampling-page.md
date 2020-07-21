---
title: Editor de transformación muestreo de fila (página muestreo) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.ROWSAMPLINGTRANSFORMATION.COLUMNS.F1
- sql12.dts.designer.rowsamplingtransformation.f1
helpviewer_keywords:
- Row Sampling Transformation Editor
ms.assetid: 544c7709-6de0-4c08-bda3-759985be9a05
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d3e75cb6d7c0e8838dc9e56241424bbf7dfe2755
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85422832"
---
# <a name="row-sampling-transformation-editor-sampling-page"></a>Editor de transformación Muestreo de fila (página Muestreo)
  Use el cuadro de diálogo **Editor de transformación Muestreo de fila** para dividir una parte de una entrada en un ejemplo que utilice un número especificado de filas. La transformación divide la entrada en dos salidas independientes.  
  
 Para obtener más información acerca de la transformación Muestreo de fila, vea [Row Sampling Transformation](data-flow/transformations/row-sampling-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Número de filas**  
 Especifique el número de filas de la entrada que se utilizarán como ejemplo.  
  
 Puede especificar el valor de esta propiedad con una expresión de propiedad.  
  
 **Nombre de salida de ejemplo**  
 Proporcione un nombre único para la salida que incluirá las filas de ejemplo. El nombre que indique se mostrará en el Diseñador SSIS.  
  
 **Nombre de salida no seleccionado**  
 Proporcione un nombre único para la salida que contendrá las filas excluidas de ejemplo. El nombre que indique se mostrará en el Diseñador SSIS.  
  
 **Utilizar el valor de inicialización aleatorio siguiente**  
 Especifique el valor de inicialización del ejemplo para el generador de números aleatorios que utiliza la transformación para crear un ejemplo. Esto solamente se recomienda para desarrollo y pruebas. La transformación utiliza el contador de Microsoft Windows como valor de inicialización si no se especifica un valor de inicialización aleatorio.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Transformación Muestreo de porcentaje](data-flow/transformations/percentage-sampling-transformation.md)  
  
  

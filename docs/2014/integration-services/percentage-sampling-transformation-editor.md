---
title: Editor de transformación muestreo de porcentaje | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.percentagesamplingtransformation.f1
helpviewer_keywords:
- Percentage Sampling Transformation Editor
ms.assetid: 2c40d804-26a3-4d35-809b-bc923d83d451
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0366ecb08281a28d43bc98639bf4b11e60aea402
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66056721"
---
# <a name="percentage-sampling-transformation-editor"></a>Editor de transformación Muestreo de porcentaje
  Use el cuadro de diálogo **Editor de transformación Muestreo de porcentaje** para dividir parte de una entrada en un ejemplo utilizando un porcentaje de filas especificado. La transformación divide la entrada en dos salidas independientes.  
  
 Para obtener más información acerca de la transformación Muestreo de porcentaje, vea [Percentage Sampling Transformation](data-flow/transformations/percentage-sampling-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Porcentaje de filas**  
 Especifique el porcentaje de filas de la entrada que se utilizarán como ejemplo.  
  
 Puede especificar el valor de esta propiedad con una expresión de propiedad.  
  
 **Nombre de salida de ejemplo**  
 Proporcione un nombre único para la salida que incluirá las filas de ejemplo. El nombre proporcionado se mostrará en el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Nombre de salida no seleccionado**  
 Proporcione un nombre único para la salida que contendrá las filas excluidas de ejemplo. El nombre proporcionado se mostrará en el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Utilizar el valor de inicialización aleatorio siguiente**  
 Especifique el valor de inicialización del ejemplo para el generador de números aleatorios que utiliza la transformación para crear un ejemplo. Esto solamente se recomienda para desarrollo y pruebas. La transformación utiliza el contador de Microsoft Windows si no se especifica el valor de inicialización.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Transformación Muestreo de fila](data-flow/transformations/row-sampling-transformation.md)  
  
  

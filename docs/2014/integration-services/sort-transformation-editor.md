---
title: Editor de transformación Ordenar | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sorttransformation.f1
helpviewer_keywords:
- Sort Transformation Editor
ms.assetid: 8ae23970-49a9-4d6d-9f15-c7074783347c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: abc74915adf0f2b3fd3ae96420dea921f28ff8e3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62878022"
---
# <a name="sort-transformation-editor"></a>Editor de transformación Ordenar
  Use el cuadro de diálogo **Editor de transformación Ordenar** para seleccionar las columnas que desea ordenar, establecer el orden y especificar si deben quitarse los duplicados.  
  
 Para obtener más información acerca de la transformación Ordenar, vea [Sort Transformation](data-flow/transformations/sort-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Active las casillas de las columnas que desea ordenar.  
  
 **Name**  
 Muestra el nombre de todas las columnas de entrada disponibles.  
  
 **Paso a través**  
 Permite indicar si la columna debe incluirse en la salida ordenada.  
  
 **Columna de entrada**  
 Seleccione de la lista de entradas disponibles las columnas para cada fila. Las selecciones se reflejan en las casillas activadas en la tabla **Columnas de entrada disponibles** .  
  
 **Alias de salida**  
 Escriba un alias para cada columna de salida. El nombre predeterminado es el de la columna de entrada, pero puede elegir cualquier nombre descriptivo único.  
  
 **Tipo de orden**  
 Permite indicar si la ordenación seguirá un orden ascendente o descendente.  
  
 **Criterio de ordenación**  
 Permite indicar el orden en que deben ordenarse las columnas. Esta característica debe establecerse manualmente para cada columna.  
  
 **Marcas de comparación**  
 Para más información sobre las opciones de comparación de cadenas, vea [Comparar datos de cadena](data-flow/comparing-string-data.md).  
  
 **Quitar filas con valores de ordenación duplicados**  
 Permite indicar si la transformación copia filas duplicadas en la salida o crea una única entrada para todos los duplicados utilizando las opciones de comparación de cadenas especificadas.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  

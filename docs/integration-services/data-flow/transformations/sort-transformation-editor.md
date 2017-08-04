---
title: "Editor de transformación Ordenar | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sorttransformation.f1
helpviewer_keywords:
- Sort Transformation Editor
ms.assetid: 8ae23970-49a9-4d6d-9f15-c7074783347c
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e5e2f2d7e377495c658ec0caaaf325bcc8550817
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="sort-transformation-editor"></a>Editor de transformación Ordenar
  Use el cuadro de diálogo **Editor de transformación Ordenar** para seleccionar las columnas que desea ordenar, establecer el orden y especificar si deben quitarse los duplicados.  
  
 Para obtener más información acerca de la transformación Ordenar, vea [Sort Transformation](../../../integration-services/data-flow/transformations/sort-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Active las casillas de las columnas que desea ordenar.  
  
 **Nombre**  
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
 Para obtener más información sobre las opciones de comparación de cadenas, vea [Comparar datos de cadena](../../../integration-services/data-flow/comparing-string-data.md).  
  
 **Quitar filas con valores de ordenación duplicados**  
 Permite indicar si la transformación copia filas duplicadas en la salida o crea una única entrada para todos los duplicados utilizando las opciones de comparación de cadenas especificadas.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)  
  
  

---
title: "Descripción de las transformaciones sincrónicas y asincrónicas | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- transformations [Integration Services], synchronous and asynchronous
- asynchronous transformations [Integration Services]
- data flow components [Integration Services], synchronous and asynchronous
- synchronous transformations [Integration Services]
ms.assetid: 0bc2bda5-3f8a-49c2-aaf1-01dbe4c3ebba
caps.latest.revision: "17"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 21d23689ec407d03f8329d628791c19beaf6243e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="understanding-synchronous-and-asynchronous-transformations"></a>Descripción de las transformaciones sincrónicas y asincrónicas
  Para entender la diferencia que existe entre una transformación sincrónica y una transformación asincrónica en [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], lo más fácil es empezar por la descripción de una transformación sincrónica. Si una transformación sincrónica no satisface sus necesidades, puede que su diseño requiera una transformación asincrónica.  
  
## <a name="synchronous-transformations"></a>Transformaciones sincrónicas  
 Una transformación sincrónica procesa las filas entrantes y se las pasa al flujo de datos de una en una. La salida es sincrónica con respecto a la entrada, lo que significa que tienen lugar al mismo tiempo. Por lo tanto, para procesar una fila determinada, la transformación no necesita información sobre otras filas del conjunto de datos. En la implementación real, las filas se agrupan en búferes cuando se pasan de un componente al siguiente, pero estos búferes son visibles para el usuario y puede suponerse que cada fila se procesa por separado.  
  
 Un ejemplo de transformación sincrónica es la transformación Conversión de datos. Para cada fila entrante, convierte el valor de la columna especificada y envía la fila a lo largo de su recorrido. Cada operación de conversión discreta es independiente del resto de las filas del conjunto de datos.  
  
 En scripting y programación de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], para especificar una transformación sincrónica, debe buscar el identificador de entrada de un componente y asignarlo a la propiedad  **SynchronousInputID** de las salidas del componente. Esto indica al motor de flujo de datos que procese cada fila de entrada y se la envíe automáticamente a las salidas especificadas. Si desea que cada fila se dirija a cada una de las salidas, no es necesario que escriba código adicional para generar los datos. Si usa la propiedad **ExclusionGroup** para especificar que las filas solo se dirijan a uno u otro de los grupos de salidas, como en el caso de la transformación División condicional, debe llamar al método **DirectRow** para seleccionar el destino adecuado para cada fila. Cuando tenga una salida de error, deberá llamar a **DirectErrorRow** para enviar las filas con problemas a la salida de error en lugar de enviarlas a la salida predeterminada.  
  
## <a name="asynchronous-transformations"></a>Transformaciones asincrónicas  
 Es posible que decida que su diseño requiere una transformación asincrónica cuando no es posible procesar cada fila independientemente del resto de las filas. En otras palabras, no es posible pasar cada fila al flujo de datos en cuanto se procesa, sino que los datos deben generarse de forma asincrónica o en un momento distinto al de la entrada. Por ejemplo, los siguientes escenarios requieren una transformación asincrónica:  
  
-   El componente debe adquirir varios búferes de datos para poder realizar su procesamiento. Un ejemplo es la transformación Ordenar, donde el componente tiene que procesar el conjunto de filas completo en una sola operación.  
  
-   El componente tiene que combinar filas de varias entradas. Un ejemplo es la transformación Mezclar, donde el componente tiene que examinar varias filas de cada entrada y, a continuación, combinarlas de forma ordenada.  
  
-   No hay una correspondencia de uno a uno entre las filas de entrada y las filas de salida. Un ejemplo es la transformación Agregado, donde el componente tiene que agregar una fila a la salida para almacenar los valores de agregado calculados.  
  
 En scripting y programación de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], para especificar una transformación asincrónica se asigna el valor 0 a la propiedad **SynchronousInputID** de las salidas del componente. . Esto indica al motor de flujo de datos que no envíe cada fila automáticamente a las salidas. A continuación, debe escribir código para enviar cada fila explícitamente a la salida adecuada agregándosela al nuevo búfer de salida que se crea para la salida de una transformación asincrónica.  
  
> [!NOTE]  
>  Puesto que un componente de origen también debe agregar explícitamente a sus búferes de salida cada una de las filas que lee del origen de datos, un origen es similar a una transformación con salidas asincrónicas.  
  
 También sería posible crear una transformación asincrónica que emule una transformación sincrónica mediante la copia explícita de cada fila de entrada en la salida. Con este enfoque, podría cambiar el nombre de las columnas o convertir los tipos de datos o los formatos. No obstante, este enfoque disminuye el rendimiento. Puede obtener los mismos resultados con un mayor rendimiento utilizando componentes integrados de Integration Services, como Copiar columna o Conversión de datos.  
  
## <a name="see-also"></a>Ver también  
 [Crear una transformación sincrónica con el componente de script](../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
 [Crear una transformación asincrónica con el componente de script](../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)   
 [Desarrollar un componente de transformación personalizado con salidas sincrónicas](../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)   
 [Desarrollar un componente de transformación personalizado con salidas asincrónicas](../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
  

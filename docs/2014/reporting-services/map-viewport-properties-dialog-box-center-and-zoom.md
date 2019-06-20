---
title: Cuadro de diálogo de propiedades de ventanilla, centro y Zoom se asignan | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.mapviewport.centerandzoom.f1
- "10506"
ms.assetid: 642a06f5-293f-48e0-97a6-1489dbefa719
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4a5c71344fe45df4265db72e9fd6dc41ac13bd98
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108291"
---
# <a name="map-viewport-properties-dialog-box-center-and-zoom"></a>Cuadro de diálogo Propiedades de ventanilla de mapa, Centrar y hacer zoom
  Seleccione **Centrar y hacer zoom** en el cuadro de diálogo **Propiedades de ventanilla de mapa** para establecer la vista de centro y el factor de zoom de un mapa. Después de especificar un origen de datos de mapa y los límites del mapa que desee incluir en el informe, puede especificar el centro de la vista y el factor de zoom para controlar más la presentación del mapa. Las opciones cambian en función de qué método se use para especificar los valores del centro y el zoom. Haga clic en el botón **Expresión** (*fx*) para modificar una expresión que establezca el valor de la opción.  
  
## <a name="options"></a>Opciones  
 **Establecer un centro de la vista y el nivel de zoom**  
 Elija esta opción para especificar los valores personalizados para el centro de la vista y el nivel de zoom.  
  
 **Centrar mapa para mostrar una capa de mapa**  
 Elija esta opción para especificar una capa y centrar automáticamente la vista en los datos del mapa. Por ejemplo, centre la vista en LineLayer1.  
  
 **Centrar mapa para mostrar un elemento de mapa incrustado**  
 Elija esta opción para centrar la vista en un elemento de mapa enlazado a datos concreto. Los datos espaciales deben tener una relación con los datos analíticos para especificar esta opción.  
  
 Por ejemplo, centre la vista en el elemento de mapa en el que el nombre del campo coincidente sea [City] y el valor de coincidencia "Seattle".  
  
 **Centrar mapa para mostrar todos los elementos de mapa enlazado a datos**  
 Elija esta opción para centrar la vista en todos los elementos de mapa de la capa. Los datos espaciales deben tener una relación con los datos analíticos para especificar esta opción.  
  
 Por ejemplo, centre la vista en la capa de burbuja de polígono que muestra las ciudades y el tamaño de burbuja se relaciona con la población. Solo las ciudades con un valor de población coincidente se incluyen al calcular el centro de la ventanilla.  
  
 **Opciones de centrar y hacer zoom**  
 Seleccione una opción para especificar el centro de la vista y el nivel de zoom.  
  
 **Vista center (X) %**  
 Coordenada horizontal. El valor predeterminado, 50%, centra la vista en el punto medio entre los valores horizontales mínimo y máximo.  
  
 **La vista Centro (Y) %**  
 Coordenada vertical. El valor predeterminado, 50%, centra la vista en el punto medio entre los valores verticales mínimo y máximo.  
  
 **Nivel de zoom (%)**  
 Factor del zoom. El valor predeterminado, 100%, indica que no se produce aumento.  
  
 **Centrar vista en esta capa**  
 Especifica el nombre de la capa.  
  
 **Centrar vista en el elemento de mapa que coincide con esta condición**  
 El campo de solo lectura que se muestra se utiliza para hacer coincidir los datos del mapa con los datos analíticos. Especifique el valor con el que desea buscar la coincidencia. La vista se centra automáticamente en este elemento del mapa. Por ejemplo, NAME = TEXAS. De forma predeterminada, el tipo de datos de la condición es String y la coincidencia distingue entre mayúsculas y minúsculas.  
  
 Para establecer la coincidencia en un campo que tiene un tipo de datos diferente, debe escribir una expresión que se evalúe como ese tipo de datos. Por ejemplo, si el campo coincidente es un código postal de cinco dígitos que se almacena como un entero, para especificar el código postal 98053, debe utilizar la expresión =98053.  
  
## <a name="see-also"></a>Vea también  
 [Mapas &#40;Generador de informes y SSRS&#41;](report-design/maps-report-builder-and-ssrs.md)  
  
  

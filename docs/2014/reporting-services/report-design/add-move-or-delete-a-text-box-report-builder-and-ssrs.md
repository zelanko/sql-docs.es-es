---
title: Agregar, mover o eliminar un cuadro de texto (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f042cf81-d933-4ac7-9287-c074a46bde98
caps.latest.revision: 5
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 2023c9a066d2a9f0e9507fe0c06dcab4fbcc66a9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201970"
---
# <a name="add-move-or-delete-a-text-box-report-builder-and-ssrs"></a>Agregar, mover o eliminar un cuadro de texto (Generador de informes y SSRS)
  Los cuadros de texto son los elementos de informe más usados en los informes. Puede agregar un cuadro de texto al cuerpo del informe para mostrar información como títulos, opciones de parámetros, campos integrados y fechas.  
  
 Cada celda de una tabla o matriz es en realidad un cuadro de texto. Casi todos los datos de informe mostrados en un informe con tablas y matrices son el resultado de la evaluación por parte del procesador de informes del contenido de cada cuadro de texto del informe. Como tal, puede dar formato a las celdas de la misma manera que daría formato a otros cuadros de texto que estuvieran fuera de la región de datos.  
  
 Para agregar un cuadro de texto a una región de datos de lista, debe agregar primero el cuadro de texto y, a continuación, arrastrarlo a la lista.  
  
> [!NOTE]  
>  Al hacer clic en un cuadro de texto, puede editar inmediatamente el texto de ese cuadro. Para seleccionar el propio cuadro de texto, no el texto que contiene, presione ESC.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-text-box"></a>Para agregar un cuadro de texto  
  
1.  En la vista Diseño, en la pestaña **Insertar** , haga clic en **Cuadro de texto**.  
  
2.  En la superficie de diseño, haga clic y, a continuación, arrastre un cuadro hasta obtener el tamaño deseado del cuadro de texto. También puede hacer clic en la superficie de diseño para crear un cuadro de texto de tamaño predeterminado.  
  
### <a name="to-add-a-text-box-in-a-list"></a>Para agregar un cuadro de texto a una lista  
  
1.  En la vista de diseño de informe, en la pestaña **Insertar** , haga clic en **Lista**.  
  
2.  En la superficie de diseño, haga clic y, a continuación, arrastre un cuadro hasta obtener el tamaño deseado de la lista. O bien, haga clic en la superficie de diseño para crear una lista de tamaño predeterminado.  
  
3.  En la pestaña **Insertar** , haga clic en **Cuadro de texto**.  
  
4.  En la superficie de diseño, haga clic en cuadro y, a continuación, arrástrelo hasta obtener el tamaño deseado dentro de la lista que agregó en el paso 1. O bien, haga clic en la superficie de diseño dentro de la lista para crear un cuadro de texto de tamaño predeterminado.  
  
5.  Para confirmar que el cuadro de texto se ha anidado correctamente dentro de la lista, selecciónelo.  
  
    > [!NOTE]  
    >  Si hace clic en el cuadro de texto y está en modo de edición, presione ESC para seleccionar el cuadro de texto.  
  
6.  En el panel Propiedades, compruebe que la propiedad **Parent** es el rectángulo que se agregó automáticamente a la región de datos de lista.  
  
    > [!NOTE]  
    >  Si el panel de propiedades no está visible, en la pestaña **Ver** seleccione **Propiedades** .  
  
### <a name="to-move-a-text-box"></a>Para mover un cuadro de texto  
  
1.  En la vista de diseño de gráfico, haga clic en un espacio vacío del cuadro de texto para seleccionarlo.  
  
    > [!NOTE]  
    >  Si hace clic en el cuadro de texto y está en modo de edición, presione ESC para seleccionar el cuadro de texto.  
  
2.  Haga clic en el identificador del cuadro de texto y arrastre el cuadro de texto a la nueva ubicación. O bien, use las teclas de dirección para mover horizontal o verticalmente un cuadro de texto seleccionado. Para mover el cuadro de texto en incrementos más pequeños en la superficie de diseño, mantenga presionada la tecla CTRL mientras usa las teclas de dirección.  
  
### <a name="to-delete-a-text-box"></a>Para eliminar un cuadro de texto  
  
1.  En la vista de diseño de gráfico, haga clic con el botón derecho en un espacio vacío del cuadro de texto para seleccionarlo y, después, haga clic en **Eliminar**. O bien, haga clic en un espacio vacío del cuadro de texto y, a continuación, presione SUPRIMIR.  
  
    > [!NOTE]  
    >  Si hace clic en el cuadro de texto y está en modo de edición, presione ESC para seleccionar el cuadro de texto.  
  
## <a name="see-also"></a>Vea también  
 [Cuadros de texto &#40;el generador de informes SSRS&#41;](text-boxes-report-builder-and-ssrs.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Métodos abreviados de teclado &#40;generador de informes&#41;](../report-builder/keyboard-shortcuts-report-builder.md)  
  
  
---
title: "Agregar un subinforme y parámetros (Generador de informes y SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10093"
- sql13.rtp.rptdesigner.subreportproperties.general.f1
ms.assetid: 94f960f8-a629-4f1e-8277-c3b8f0680d98
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 2ad2eeac8c2758be74150e0ccbb262beb39ef3af
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="add-a-subreport-and-parameters-report-builder-and-ssrs"></a>Agregar un subinforme y parámetros (Generador de informes y SSRS)
  Agregue subinformes a un informe cuando desee crear un informe principal que actúe como contenedor para varios informes relacionados. Un subinforme es una referencia a otro informe. Para relacionar informes mediante valores de datos (por ejemplo, para que varios informes muestren datos del mismo cliente), debe diseñar un informe con parámetros (por ejemplo, un informe que muestre los detalles de un cliente concreto) como el subinforme. Al agregar un subinforme al informe principal, puede especificar los parámetros que se deben pasar al subinforme.  
  
 También puede agregar subinformes a filas o columnas dinámicas de una tabla o matriz. Cuando se procesa el informe principal, se procesa el subinforme para cada fila. En este caso, considere la posibilidad de lograr el efecto deseado usando regiones de datos o regiones de datos anidadas.  
  
 Para agregar un subinforme a un informe, primero debe crear el informe que actuará como el subinforme. Para obtener más información sobre la creación del subinforme, vea [Subinformes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-subreport"></a>Agregar un subinforme  
  
1.  En la pestaña **Insertar** , haga clic en **Subinforme**.  
  
2.  En la superficie de diseño, haga clic en una ubicación en el informe y, a continuación, arrastre un cuadro hasta que alcance el tamaño deseado para el subinforme. O bien, haga clic en la superficie de diseño para crear un subinforme de tamaño predeterminado.  
  
3.  Haga clic con el botón derecho en el subinforme y, después, haga clic en **Propiedades del subinforme**.  
  
4.  En el cuadro de diálogo **Propiedades del subinforme** , escriba un nombre en el cuadro de texto **Nombre** o acepte el valor predeterminado. El nombre debe ser único en el informe. De forma predeterminada, se asigna un nombre general como Subreport1 o Subreport2.  
  
5.  En el cuadro **Usar este informe como un subinforme** , escriba el nombre del informe o haga clic en **Examinar**. Es preferible hacer clic en **Examinar** , porque la ruta de acceso al subinforme se especificará automáticamente. El informe se puede especificar de varias maneras. Para más información, vea [Especificar las rutas de acceso a los elementos externos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
6.  (Opcional) Haga clic en **Sí** para **Omitir borde en el salto de página** , para impedir que un borde se represente en mitad del subinforme si este abarca más de una página.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-specify-parameters-to-pass-to-a-subreport"></a>Especificar los parámetros que se pasarán a un subinforme  
  
1.  En la vista de diseño, haga clic con el botón derecho en el subinforme y, después, haga clic en **Propiedades del subinforme**.  
  
2.  En el cuadro de diálogo **Propiedades del subinforme** , haga clic en **Agregar**.  
  
3.  Haga clic en **Agregar**. Se agrega una nueva fila a la cuadrícula de parámetros.  
  
4.  En el cuadro de texto **Nombre** , escriba el nombre de un parámetro en el subinforme o elíjalo del cuadro de lista. Este nombre debe coincidir con un parámetro de informe del subinforme, no con un parámetro de consulta.  
  
5.  En el cuadro de lista **Valor** , escriba o seleccione el valor que se pasará al subinforme. Este valor puede ser texto estático o una expresión que haga referencia a un campo o a otro objeto del informe principal.  
  
    > [!NOTE]  
    >  En el Generador de informes, si falta un parámetro de la lista **Parámetros** y se ha definido un valor predeterminado para el subinforme, este se procesará correctamente.  
    >   
    >  En el Diseñador de informes, todos los parámetros que requiera el subinforme deben incluirse en la lista **Parámetros** . Si falta un parámetro necesario, el subinforme no se muestra correctamente en el informe principal.  
  
6.  Repita los pasos 3 y 5 para especificar un nombre y un valor para cada parámetro del subinforme.  
  
7.  Para eliminar un parámetro de subinforme, haga clic en el parámetro en la cuadrícula de parámetros y, a continuación, haga clic en **Eliminar**.  
  
8.  Para cambiar el orden de un parámetro del subinforme, selecciónelo y, después, haga clic en el botón Subir o Bajar.  
  
     Cambiar el orden de un parámetro de subinforme no afecta al procesamiento del subinforme.  
  
## <a name="see-also"></a>Vea también  
 [Subinformes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md)   
 [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)  
  
  

---
title: Agregar una acción de obtención de detalles en un informe (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 153729c4-d01e-4629-b78f-0cfd5a7f83da
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a345b0ed36fde93a3bc94ff4075233c6c24728af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66106867"
---
# <a name="add-a-drillthrough-action-on-a-report-report-builder-and-ssrs"></a>Agregar una acción de obtención de detalles en un informe (Generador de informes y SSRS)
  El informe que se abre al hacer clic en el vínculo del informe principal se denomina *informe detallado*. Este vínculo de obtención de detalles habilita una acción de obtención de detalles.  
  
 Los informes detallados deben publicarse en el mismo servidor de informes que el informe principal, pero pueden estar en carpetas diferentes. Puede agregar un vínculo de obtención de detalles a cualquier elemento que tenga una propiedad **Action** , como un cuadro de texto, una imagen o los puntos de datos de un gráfico.  
  
 Para agregar un vínculo de obtención de detalles a un informe, debe crear primero el informe detallado al que se vinculará el informe principal. Un informe detallado contiene normalmente los detalles sobre un elemento que está incluido en el informe de resumen original y a menudo contiene los parámetros que filtran el informe detallado en función de los parámetros que han pasado a él desde el informe principal. Para más información sobre cómo crear el informe detallado, vea [Informes detallados &#40;Generador de informes y SSRS&#41;](drillthrough-reports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-drillthrough-action"></a>Para agregar una acción de obtención de detalles  
  
1.  En la vista Diseño, haga clic con el botón derecho en el gráfico, la imagen o el cuadro de texto al que quiere agregar el vínculo y, después, haga clic en **Propiedades**.  
  
2.  En el cuadro de diálogo **Propiedades** del elemento, haga clic en **Acción**.  
  
3.  Seleccione **Ir a informe**. Aparecen secciones adicionales en el cuadro de diálogo para esta opción.  
  
4.  En **Especificar un informe**, haga clic en **Examinar** para localizar el informe al que desea ir o escriba el nombre del informe. O bien, puede hacer clic en el botón de la expresión (**fx**) para crear una expresión para el nombre del informe.  
  
     El formato de la ruta de acceso al informe detallado difiere para el modo nativo y para el modo integrado en SharePoint. Si busca el informe, se proporcionará una ruta de acceso con el formato correcto. Para más información, vea [Especificar las rutas de acceso a los elementos externos &#40;Generador de informes y SSRS&#41;](specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
     Si tiene que especificar parámetros para el informe detallado, siga el paso siguiente.  
  
5.  En **Utilizar estos parámetros para ejecutar el informe**, haga clic en **Agregar**. Se agrega una nueva fila a la cuadrícula de parámetros.  
  
    -   En el cuadro de texto **Nombre** , haga clic en la lista desplegable o escriba el nombre del parámetro de informe del informe detallado.  
  
        > [!NOTE]  
        >  Los nombres de la lista de parámetros deben coincidir exactamente con los parámetros previstos en el informe de destino. Por ejemplo, los nombres de parámetro deben coincidir en mayúsculas y minúsculas. Si los nombres no coinciden o si en la lista falta algún parámetro previsto, se produce un error en el informe detallado.  
  
    -   En **Valor**, escriba o seleccione el valor que se va a pasar al parámetro del informe detallado.  
  
        > [!NOTE]  
        >  Los valores pueden contener una expresión que se evalúe como un valor que se pasará al parámetro de informe. En la lista de valores, las expresiones incluyen la lista de campos del informe actual.  
  
     Para información sobre cómo ocultar parámetros en informes, vea [Agregar, cambiar o eliminar parámetros de informe &#40;Generador de informes y SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md).  
  
6.  (Opcional) En los cuadros de texto, resulta útil cambiar el color y el efecto del texto en la pestaña **Inicio** de la cinta de opciones para indicar al usuario que el texto es un vínculo.  
  
7.  Para probar el vínculo, ejecute el informe y haga clic en el elemento de informe en el que ha establecido este vínculo.  
  
## <a name="see-also"></a>Consulte también  
 [Cuadro de diálogo Propiedades de acción &#40;Generador de informes y SSRS&#41;](../action-properties-dialog-box-report-builder-and-ssrs.md)   
 [Aplicar formato a los puntos de datos de un gráfico &#40;Generador de informes y SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Mostrar la información sobre herramientas en una serie &#40;Generador de informes y SSRS&#41;](show-tooltips-on-a-series-report-builder-and-ssrs.md)  
  
  

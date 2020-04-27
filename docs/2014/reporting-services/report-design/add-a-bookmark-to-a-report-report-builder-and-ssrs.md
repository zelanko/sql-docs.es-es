---
title: Agregar un marcador a un informe (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f130562e-5673-40e3-8e01-de7227a21d41
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0031e215c0674f87620e283a7bf903b174a40ae3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106918"
---
# <a name="add-a-bookmark-to-a-report-report-builder-and-ssrs"></a>Agregar un marcador a un informe (Generador de informes y SSRS)
  Agregue marcadores y vínculos de marcador a un informe si desea incluir una tabla de contenido personalizada o vínculos de navegación interna personalizados en el informe. Normalmente, se agregan marcadores a las ubicaciones del informe a las que se desea dirigir a los usuarios, como las tablas, los gráficos o los valores de grupo únicos mostrados en una tabla o matriz. Puede crear sus propias cadenas para usarlas como marcadores o, para los grupos, puede establecer el marcador en la expresión de grupo.  
  
 Una vez creados los marcadores, puede agregar elementos de informe en los que el usuario puede hacer clic para desplazarse a cada marcador. Normalmente, estos elementos son cuadros de texto o imágenes.  
  
 Por ejemplo, si el informe muestra una tabla agrupada por color, podría agregar un marcador basado en la expresión de grupo al encabezado de grupo. A continuación, agregaría una tabla con un único cuadro de texto al principio del informe que mostrase los valores de color y establecería el vínculo de marcador en dicho cuadro de texto. Al hacer clic en el color, el informe saltará a la página que muestra la fila del encabezado de grupo para ese color.  
  
 Puede agregar un marcador a cualquier elemento de informe y un vínculo de marcador a cualquier elemento que tenga una propiedad **Action** , como por ejemplo, un cuadro de texto, una imagen o una serie calculada en un gráfico. Para más información vea [Cuadro de diálogo Propiedades de acción &#40;Generador de informes y SSRS&#41;](../action-properties-dialog-box-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-bookmark"></a>Para agregar un marcador  
  
1.  En la vista de diseño de informe, seleccione el cuadro de texto, la imagen, el gráfico o el elemento de informe al que desea agregar un marcador. Las propiedades del elemento seleccionado aparecen en el panel de propiedades.  
  
2.  En el cuadro de texto situado junto a **Marcador**, escriba una cadena que será la etiqueta de este marcador. Por ejemplo, podría escribir **BikePhoto** como marcador para una imagen en el informe. También puede hacer clic en el botón Expresión (**fx**) para abrir el cuadro de diálogo **Expresión** y especificar una expresión que dé como resultado una etiqueta. En el caso de un grupo, la expresión usada debería ser la expresión de grupo.  
  
    > [!NOTE]  
    >  El marcador puede ser cualquier cadena, pero debe ser única en el informe. Si el marcador no es único, el vínculo a ese marcador encontrará el primer marcador que coincida.  
  
### <a name="to-add-a-bookmark-link"></a>Para agregar un vínculo de marcador  
  
1.  En la vista Diseño, haga clic con el botón derecho en el gráfico, la imagen o el cuadro de texto donde quiere agregar el vínculo y, después, haga clic en **Propiedades**.  
  
2.  En el cuadro de diálogo **Propiedades** que aparece para ese elemento de informe, haga clic en **Action**.  
  
3.  Seleccione **Ir a marcador**. Aparece una sección adicional en el cuadro de diálogo para esta opción.  
  
4.  En el cuadro **Seleccionar marcador** , escriba o seleccione un marcador o una expresión que se evalúe como un marcador. Con el ejemplo anterior, escriba **BikePhoto** para crear un vínculo a la imagen en el informe.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  (Opcional) El texto no recibe automáticamente el formato de vínculo. En el caso del texto, resulta útil cambiar el color y el efecto del texto para indicar que el texto es un vínculo. Por ejemplo,puede cambiar el color a azul y el efecto a subrayado en la sección **Fuente** de la pestaña Inicio de la cinta.  
  
7.  Para probar el vínculo, haga clic en **Ejecutar** para obtener la vista previa del informe y, a continuación, haga clic en el elemento de informe en el que ha establecido este vínculo.  
  
## <a name="see-also"></a>Consulte también  
 [Ordenación interactiva, mapas de documento y vínculos &#40;Generador de informes y SSRS&#41;](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  

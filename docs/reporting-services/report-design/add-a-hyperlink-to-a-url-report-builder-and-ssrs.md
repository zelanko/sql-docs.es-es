---
title: Agregar un hipervínculo a una dirección URL (Generador de informes y SSRS) | Microsoft Docs
ms.date: 09/07/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: d3392c0b-7b62-4d27-bc04-2bd0c5487d08
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 756cde54f9379ad5caabedfe9b0adcace65b1605
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43277475"
---
# <a name="add-a-hyperlink-to-a-url-report-builder-and-ssrs"></a>Agregar un hipervínculo a una dirección URL (Generador de informes y SSRS)
Aprenda a agregar acciones de hipervínculo a cuadros de texto, imágenes, gráficos y medidores en informes paginados de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]  . Los vínculos pueden ir a otros informes, a los marcadores de un informe o a direcciones URL estáticas o dinámicas. 

 Puede agregar un hipervínculo a cualquier elemento que tenga una propiedad **Acción** , como por ejemplo, un cuadro de texto, una imagen o una serie calculada en un gráfico. Cuando el usuario haga clic en el elemento de informe, tendrá lugar la acción que haya definido.  
  
*   Puede **agregar un hipervínculo que se abrirá un explorador con una dirección URL** que especifique. El hipervínculo puede ser una dirección URL estática o una expresión que se evalúe como una dirección URL. Si un campo de una base de datos contiene direcciones URL, una expresión pueden contener dicho campo, lo que dará lugar a una lista dinámica de hipervínculos en el informe. Asegúrese de que los lectores del informe tienen acceso a la dirección URL proporcionada.  
   
*  También puede **especificar direcciones URL para llevar a cabo obtenciones de detalles** en informes situados en cualquier servidor de informes para el que usted y sus usuarios tengan permiso para ver mediante solicitudes URL. Por ejemplo, puede especificar un informe y ocultar el mapa del documento para los usuarios cuando vean el informe por primera vez. Para obtener más información, vea [Acceso URL &#40;SSRS&#41;](../../reporting-services/url-access-ssrs.md) y [Especificar las rutas de acceso a los elementos externos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).
 
 *  Y puede **agregar un marcador a un lugar específico** en el mismo informe. 
  
Intente agregar hipervínculos con los datos de ejemplo incluidos en [Tutorial: Dar formato a texto &#40;(Generador de informes)&#41;](../../reporting-services/tutorial-format-text-report-builder.md).  
  
> [!NOTE]  
>  Los vínculos que se enlazan a los campos de conjunto de datos pueden ser vulnerables a la alteración con fines malintencionados. Para obtener más información, vea [Proteger informes y recursos](../../reporting-services/security/secure-reports-and-resources.md).  
  
## <a name="to-add-a-hyperlink-and"></a>Para agregar un hipervínculo y...   
  
1.  En la vista de diseño de informes, haga clic con el botón derecho en el gráfico, la imagen o el cuadro de texto al que quiere agregar el vínculo y, después, haga clic en **Propiedades**.  
  
2.  En el cuadro de diálogo Propiedades, haga clic en la pestaña **Acción** . Lea para obtener información sobre las opciones.  

## <a name="-add-drillthrough-to-another-report"></a>...agregar obtención de detalles a otro informe

1. En la pestaña **Acción** , seleccione **Ir a informe**. 

2. Especifique el informe de destino y los parámetros que desea usar. Los nombres de los parámetros deben coincidir con los de los parámetros definidos para el informe de destino. 

3. Use los botones **Agregar** y **Eliminar** para agregar y quitar parámetros, y las flechas hacia arriba y hacia abajo para ordenar la lista de parámetros.

4.  En **Valor** , escriba o seleccione un valor que debe pasarse al parámetro especificado para el informe detallado. Haga clic en el botón Expresión (fx) para editar la expresión.

5. Seleccione **Omitir** para impedir que el parámetro se ejecute. De forma predeterminada, esta casilla está desactivada. Para activar la casilla, haga clic en el botón Expresión (fx) y escriba True o cree una expresión. La casilla se activa al hacer clic en **Aceptar** en el cuadro de diálogo Expresión.
  
   Para obtener más información, vea [Agregar una acción de obtención de detalles en un informe](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md) . 
   
6. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
   
## <a name="-add-a-bookmark"></a>...agregar un marcador

Puede crear vínculos a marcadores en una ubicación en el informe actual. Para crear un vínculo a un marcador, debe definir primero la propiedad **Marcador** de un elemento de informe. Para definir la propiedad **Marcador** , seleccione un elemento de informe y, en el panel Propiedades, escriba un valor o expresión para el identificador de marcador; por ejemplo, SalesChart o 5TopSales.

1. En la pestaña **Acción** , seleccione **Ir a marcador**. 

2. Escriba o seleccione el identificador de marcador al que debe saltar el informe. Haga clic en el botón Expresión (fx) para modificar la expresión. 

   El identificador de marcador puede ser un identificador estático o una expresión que se evalúa como un identificador de marcador. La expresión puede incluir un campo que contenga un identificador de marcador.
   
   Para obtener más información, consulte [Agregar un marcador a un informe](../../reporting-services/report-design/add-a-bookmark-to-a-report-report-builder-and-ssrs.md) .
   
3. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="-add-a-hyperlink"></a>...agregar un hipervínculo 
  
1. En la pestaña **Acción** , seleccione **Ir a dirección URL**. Aparece una sección adicional en el cuadro de diálogo para esta opción.  
  
4.  En **Seleccionar dirección URL**, escriba o seleccione una dirección URL o una expresión que se evalúe como una dirección URL, o haga clic en la flecha de lista desplegable y haga clic en el nombre de un campo que contenga una dirección URL. 

    En el caso de un elemento publicado en un servidor de informes configurado para el modo nativo, use una ruta de acceso completa o relativa. Por ejemplo, `http://<servername>/images/image1.jpg`. 
    
    En el caso de un elemento publicado en un servidor de informes configurado en el modo integrado de SharePoint, use una dirección URL completa. Por ejemplo, `http://<SharePointservername>/<site>/Documents/images/image1.jpg`.
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="after-you-add-a-hyperlink"></a>Después de agregar un hipervínculo
  
1.  (Opcional) El texto no recibe automáticamente el formato de vínculo. En el caso del texto, resulta útil cambiar el color y el efecto del texto para indicar que el texto es un vínculo. Por ejemplo,puede cambiar el color a azul y el efecto a subrayado en la sección **Fuente** de la pestaña Inicio de la cinta.  
  
7.  Para probar el vínculo, haga clic en **Ejecutar** para obtener la vista previa del informe y, a continuación, haga clic en el elemento de informe en el que ha establecido este vínculo.  
  
## <a name="see-also"></a>Ver también  
 [Ordenación interactiva, mapas de documento y vínculos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Crear un mapa del documento &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/create-a-document-map-report-builder-and-ssrs.md)  
  
  

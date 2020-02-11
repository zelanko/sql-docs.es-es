---
title: Agregar un hipervínculo a una dirección URL (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d3392c0b-7b62-4d27-bc04-2bd0c5487d08
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6fa7b0d32a62e5e2d729e05c88b892ccaffc0fc2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66106815"
---
# <a name="add-a-hyperlink-to-a-url-report-builder-and-ssrs"></a>Agregar un hipervínculo a una dirección URL (Generador de informes y SSRS)
  Puede agregar un hipervínculo a un elemento de informe si desea que los usuarios puedan hacer clic en un vínculo de un informe y abrir el explorador para la dirección URL especificada. Los hipervínculos pueden ser una dirección URL estática o una expresión que se evalúe como una dirección URL. Si un campo de una base de datos contiene direcciones URL, una expresión pueden contener dicho campo, lo que dará lugar a una lista dinámica de hipervínculos en el informe. Puede agregar hipervínculos a cuadros de texto, imágenes, gráficos y medidores. Debe asegurarse de que los usuarios tienen acceso a la dirección URL proporcionada.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 También puede especificar direcciones URL a los informes situados en cualquier servidor de informes para el que usted y sus usuarios tengan permiso para ver mediante solicitudes URL. Por ejemplo, puede especificar un informe y ocultar el mapa del documento para los usuarios cuando vean el informe por primera vez. Para más información, vea [Acceso URL &#40;SSRS&#41;](../url-access-ssrs.md) en la [documentación de Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Puede agregar un hipervínculo a una dirección URL a cualquier elemento que tenga una propiedad **Acción** , como por ejemplo, un cuadro de texto, una imagen o una serie calculada en un gráfico. Cuando el usuario haga clic en el elemento de informe, tendrá lugar la acción que haya definido. Para más información, vea [Cuadro de diálogo Propiedades de acción &#40;Generador de informes y SSRS&#41;](../action-properties-dialog-box-report-builder-and-ssrs.md) y [Especificar las rutas de acceso a los elementos externos &#40;Generador de informes y SSRS&#41;](specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
 Para más información, vea [Tutorial: Dar formato a texto &#40;Generador de informes&#41;](../tutorial-format-text-report-builder.md).  
  
> [!NOTE]  
>  Los vínculos que se enlazan a los campos de conjunto de datos pueden ser vulnerables a la alteración con fines malintencionados. Para más información, vea [Proteger informes y recursos](../security/secure-reports-and-resources.md) en los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][Libros en pantalla](https://go.microsoft.com/fwlink/?LinkId=154888) en msdn.microsoft.com.  
  
### <a name="to-add-a-hyperlink"></a>Para agregar un hipervínculo  
  
1.  En la vista de diseño de informes, haga clic con el botón derecho en el gráfico, la imagen o el cuadro de texto al que quiere agregar el vínculo y, después, haga clic en **Propiedades**.  
  
2.  En el cuadro de diálogo Propiedades, haga clic en **Acción**.  
  
3.  Seleccione **Ir a dirección URL**. Aparece una sección adicional en el cuadro de diálogo para esta opción.  
  
4.  En **Seleccionar dirección URL**, escriba o seleccione una dirección URL o una expresión que se evalúe como una dirección URL, o haga clic en la flecha de lista desplegable y haga clic en el nombre de un campo que contenga una dirección URL.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  (Opcional) El texto no recibe automáticamente el formato de vínculo. En el caso del texto, resulta útil cambiar el color y el efecto del texto para indicar que el texto es un vínculo. Por ejemplo,puede cambiar el color a azul y el efecto a subrayado en la sección **Fuente** de la pestaña Inicio de la cinta.  
  
7.  Para probar el vínculo, haga clic en **Ejecutar** para obtener la vista previa del informe y, a continuación, haga clic en el elemento de informe en el que ha establecido este vínculo.  
  
## <a name="see-also"></a>Consulte también  
 [Ordenación interactiva, mapas de documento y vínculos &#40;Generador de informes y SSRS&#41;](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Crear un mapa del documento &#40;Generador de informes y SSRS&#41;](create-a-document-map-report-builder-and-ssrs.md)  
  
  

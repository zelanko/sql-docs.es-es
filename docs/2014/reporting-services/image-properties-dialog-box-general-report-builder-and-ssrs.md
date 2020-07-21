---
title: Cuadro de diálogo Propiedades de la imagen, general (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10051"
- sql12.rtp.rptdesigner.pictureproperties.general.f1
ms.assetid: c2218b93-f7fe-46ef-995f-d7dadf9752ec
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8a66c424bfe5bd4a2587140a0f5238f46833a061
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109027"
---
# <a name="image-properties-dialog-box-general-report-builder-and-ssrs"></a>Cuadro de diálogo de Propiedades de la imagen, General (Generador de informes y SSRS)
  Seleccione **General** en el cuadro de diálogo **Propiedades de la imagen** para agregar una imagen, cambiar el nombre predeterminado de la imagen y agregar texto de información sobre herramientas.  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Escriba el nombre del elemento. El nombre debe ser único en el informe. De forma predeterminada, se asigna un nombre general como Image1 o Image2.  
  
 **Herramienta**  
 Escriba texto o una expresión que dé como resultado una información sobre herramientas. Haga clic en el botón Expresión (*fx*) para editar la expresión. La **información sobre herramientas** aparece cuando el usuario pausa el puntero sobre el elemento en un informe HTML.  
  
 **Seleccionar el origen de la imagen**  
 Indique dónde se encuentra almacenada la imagen para que al representar el informe, el procesador de informes sepa dónde puede obtenerla.  
  
-   **Externo** : elija esta opción si desea que la imagen continúe existiendo como archivo en un servidor de informes o en un servidor web.  
  
-   **Incrustada** : elija esta opción si desea incrustar la imagen en el informe.  
  
-   **Base de datos** : elija esta opción si desea incluir un nombre de campo de base de datos que representa las imágenes que se van a incluir en el informe seleccionado.  
  
 **Usar esta imagen**  
 Esta opción aparece al seleccionar la opción **Incrustada** o **Externo** .  
  
 Si va a incrustar la imagen, elija la imagen que desea agregar al informe en la lista desplegable. Haga clic en el botón **Importar** para agregar la imagen a la lista desplegable.  
  
 Si selecciona la opción **Externo** , escriba la dirección URL de la imagen. En el caso de un informe publicado en un servidor de informes configurado para el modo nativo, use una ruta de acceso completa o relativa. Por ejemplo, http://\<ServerName>/images/image1.jpg. En el caso de un informe publicado en un servidor de informes configurado en el modo integrado de SharePoint, utilice una dirección URL completa. Por ejemplo, http://\<*SharePointservername*>/\<*site*>/Documents/images/image1.jpg.  
  
 **Importar**  
 Haga clic en esta opción para agregar una imagen a la lista desplegable **Usar esta imagen** .  
  
 **Usar este campo**  
 Esta opción aparece si selecciona la opción **Base de datos** . Seleccione el nombre del campo.  
  
 **Usar este tipo MIME**  
 Elija el formato adecuado de las imágenes contenidas en la base de datos (por ejemplo, .bmp, .jpeg, .gif, .png y .x-png).  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [Imágenes &#40;Generador de informes y SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [Ayuda del Generador de informes para cuadros de diálogo, paneles y asistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)  
  
  

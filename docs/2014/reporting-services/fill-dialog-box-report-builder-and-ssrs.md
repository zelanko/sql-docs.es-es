---
title: Rellenar el cuadro de diálogo (generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportbody.fill.f1
- "10065"
- "10501"
- sql12.rtp.rptdesigner.shared.filldv.f1
- sql12.rtp.rptdesigner.rectangleproperties.fill.f1
- "10064"
- sql12.rtp.rptdesigner.textboxproperties.fill.f1
- "10124"
ms.assetid: 93a91d02-d558-4a0e-8d17-3fdf21e208d3
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 35c8786c571936a27570166c8d331cbd2a641b76
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48204655"
---
# <a name="fill-dialog-box-report-builder-and-ssrs"></a>Cuadro de diálogo Relleno (Generador de informes y SSRS)
  En la pestaña **Relleno** , puede especificar opciones de color para el fondo de una o varias celdas dentro de una región de datos o de un cuadro de texto.  
  
## <a name="options"></a>Opciones  
 **Color de relleno**  
 Haga clic en el botón de color para seleccionar un color de relleno para el rectángulo. Haga clic en el **Expression***(fx)* botón para editar la expresión, que puede ser un valor hexadecimal para el color RGB o uno de los nombres de colores predefinidos que se proporcionan en el **expresión** cuadro de diálogo. Para ver una lista de los colores predefinidos, seleccione **Web** en el panel **Elemento**. Los nombres de colores del panel **Título** pueden escribirse en el panel de texto de expresiones. No use el signo igual (=) ni comillas ("") cuando escriba el nombre del color.  
  
 **Seleccione el origen de imagen**  
 Indique dónde se encuentra almacenada la imagen para que, a la hora de representar el informe, el procesador de informes pueda mostrarla.  
  
-   **Externo** : elija esta opción si desea que la imagen continúe existiendo como archivo en un servidor de informes o en un servidor web.  
  
-   **Incrustada** : elija esta opción si desea incrustar la imagen en el informe.  
  
-   **Base de datos** : elija esta opción si desea incluir un nombre de campo de base de datos que representa las imágenes que se van a incluir en el informe seleccionado.  
  
 **Usar esta imagen**  
 Esta opción aparece al seleccionar la opción **Incrustada** o **Externo** .  
  
 Si va a incrustar la imagen, elija la imagen que quiere agregar al informe en la lista desplegable. Haga clic en **Importar** para agregar la imagen a la lista desplegable. Si agregó una imagen al panel **Datos** , podrá seleccionarla eligiendo **Incrustada** y seleccionando la imagen en la lista desplegable.  
  
 Si selecciona la opción **Externo** , escriba la dirección URL de la imagen. Un informe publicado en un servidor de informes configurado para el modo nativo, use una ruta de acceso completa o relativa (por ejemplo, http://*\<servername >*/images/image1.jpg). Un informe publicado en un servidor de informes configurado en modo integrado de SharePoint, use una dirección URL completa (por ejemplo, http://*\<Nombredeservidorsharepoint > /\<sitio >*  /documentos/images / Image1.jpg).  
  
 **Importar**  
 Esta opción está disponible cuando se selecciona **Incrustada**. Haga clic en esta opción para agregar una imagen a la lista desplegable **Usar esta imagen** .  
  
 **Utilice este campo**  
 Esta opción está disponible cuando se selecciona **Base de datos**. Seleccione el nombre del campo.  
  
 **Use este tipo MIME**  
 Elija el formato adecuado de las imágenes contenidas en la base de datos (por ejemplo, .bmp, .jpeg, .gif, .png o .x-png).  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a los elementos de informe &#40;Generador de informes y SSRS&#41;](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [Aplicar formato a texto y marcadores de posición &#40;generador de informes y SSRS&#41;](report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Imágenes &#40;generador de informes y SSRS&#41;](report-design/images-report-builder-and-ssrs.md)  
  
  

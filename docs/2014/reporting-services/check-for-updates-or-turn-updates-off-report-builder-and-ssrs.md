---
title: Comprobación de actualizaciones o desactivar actualizaciones (generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 9c69792d-d7c4-453b-ae2f-6d2d071d8606
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: ace2df07f5fa0b7f696ba946771f4418702e3d42
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2019
ms.locfileid: "56296193"
---
# <a name="check-for-updates-or-turn-updates-off-report-builder-and-ssrs"></a>Buscar o desactivar actualizaciones (Generador de informes y SSRS)
  Cada vez que abre un informe, el Generador de informes comprueba si las instancias publicadas de los elementos de informe se han actualizado en el servidor de informes o en el sitio de SharePoint integrado con un servidor de informes. También comprueba los cambios de los elementos dependientes de elementos de informe, como el conjunto de datos y los parámetros. Si algún elemento de informe o sus dependencias se han actualizado en el servidor o en el sitio, una barra de información del informe muestra el número de componentes actualizados. Puede elegir ver, y aceptar o rechazar las actualizaciones, o bien descartar la barra de información.  
  
 Puede deshabilitar la barra de información y no recibir información sobre los cambios de las instancias publicadas de elementos de informe. Esta es una configuración de usuario; se deshabilitará para todos los informes que abra. Aunque haya deshabilitado la barra de información, aún puede comprobar las actualizaciones.  
  
### <a name="to-turn-on-and-off-report-part-updates"></a>Para activar y desactivar las actualizaciones de elementos de informe  
  
1.  Haga clic en el botón Generador de informes y, a continuación, haga clic en **opciones**.  
  
2.  En el **opciones** cuadro de diálogo el **recursos** ficha, active o desactive el **Mostrar actualizaciones de elementos de informe en Mis informes** casilla de verificación.  
  
> [!NOTE]  
>  Se trata de una opción de usuario. Estará deshabilitada en todos los informes que abra.  
  
### <a name="to-check-for-updates"></a>Para comprobar si hay actualizaciones  
  
-   Haga clic en la superficie de diseño fuera del informe o en el cuerpo del informe y haga clic en **buscar actualizaciones**.  
  
## <a name="see-also"></a>Vea también  
 [Elementos de informe &#40;Generador de informes y SSRS&#41;](report-parts-report-builder-and-ssrs.md)   
 [Publicar y volver a publicar elementos de informe &#40;generador de informes y SSRS&#41;](report-design/publish-and-republish-report-parts-report-builder-and-ssrs.md)   
 [Buscar elementos de informe y establecer una carpeta predeterminada &#40;generador de informes y SSRS&#41;](report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)   
 [Solucionar problemas de elementos de informe &#40;generador de informes y SSRS&#41;](../../2014/reporting-services/troubleshoot-report-parts-report-builder-and-ssrs.md)   
 [Elementos de informe y conjuntos de datos en el Generador de informes](report-data/report-parts-and-datasets-in-report-builder.md)  
  
  

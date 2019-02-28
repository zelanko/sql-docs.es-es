---
title: Especificar las rutas de acceso a los elementos externos (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 4fe513da-f3c5-479c-9fec-8662b91a0d6d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ce654cc4724a71be36e49be71bdaf64994812567
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2019
ms.locfileid: "56293486"
---
# <a name="specifying-paths-to-external-items-report-builder-and-ssrs"></a>Especificar las rutas de acceso a los elementos externos (Generador de informes y SSRS)
  Especifique rutas de acceso en las propiedades de los elementos de informe para hacer referencia a elementos tales como informes detallados, subinformes y archivos de imagen que son externos al archivo de definición de informe y se guardan en un servidor de informes.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
> [!NOTE]  
>  En el Generador de informes, las rutas de acceso a los elementos deben especificar los elementos en un servidor de informes. No se admiten las rutas de acceso a los elementos que están en un sistema de archivos. Puede obtener una vista previa de un informe que solamente utilice estos elementos si está conectado al servidor de informes donde se encuentran los elementos.  
  
 Al especificar una ruta de acceso para un elemento externo en un cuadro de diálogo de acciones, subinformes o imágenes, puede ir directamente al servidor de informes y seleccionar el elemento. Se recomienda ir a un elemento y seleccionarlo directamente para especificar un informe detallado o subinforme. De esa forma, los nombres de parámetro correctos estarán disponibles en una lista desplegable al especificar los parámetros de un informe o un subinforme. Al cambiar una ruta de acceso a un elemento para que señale a un elemento diferente, debe actualizar manualmente los valores y nombres de parámetro correctos según corresponda.  
  
 En un servidor de informes configurado en modo nativo, especifique un nombre de informe detallado sin la extensión de archivo .rdl.  
  
 En un servidor de informes configurado en modo integrado de SharePoint, debe incluir la extensión de archivo .rdl. La ruta de acceso puede ser una de las siguientes:  
  
-   **Una ruta de acceso relativa al elemento desde el informe principal.** Por ejemplo, ../TodosLosSubinformes/Subinforme1. En este ejemplo, el signo **..** indica la carpeta que está encima de aquella donde se encuentra el informe principal.  
  
    > [!NOTE]  
    >  No se admiten las rutas de acceso relativas cuando el informe se ejecuta dentro del Generador de informes. Para ver un informe que usa rutas de acceso relativas a los elementos externos, guárdelo en el servidor de informes y ejecútelo desde allí  
  
-   **Una ruta de acceso completa al elemento.**  
  
    -   **En un servidor de informes:** la ruta de acceso completa se inicia en **/**, la carpeta Inicio. Por ejemplo, /Informes/TodosLosSubinformes/Subinforme1.  
  
    -   **En un sitio de SharePoint:** debe especificar el nombre del informe en una expresión, con la dirección URL completa del elemento y la extensión de archivo .rdl. Por ejemplo, `="https://server/site/library/folder/Report1.rdl"`.  
  
## <a name="see-also"></a>Consulte también  
 [Agregar una imagen externa &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-an-external-image-report-builder-and-ssrs.md)   
 [Agregar un subinforme y parámetros &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-a-subreport-and-parameters-report-builder-and-ssrs.md)   
 [Agregar una acción de obtención de detalles en un informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md)  
  
  

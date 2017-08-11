---
title: Especificar las rutas de acceso a los elementos externos (generador de informes y SSRS) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4fe513da-f3c5-479c-9fec-8662b91a0d6d
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3ba2c751b7f851fa9be24ca08cb4ab95f4314258
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

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
  
    -   **En un servidor de informes:** la ruta de acceso empieza desde **/**, la carpeta particular. Por ejemplo, /Informes/TodosLosSubinformes/Subinforme1.  
  
    -   **En un sitio de SharePoint** : debe especificar el nombre del informe en una expresión, con la dirección URL completa del elemento y la extensión de archivo .rdl. Por ejemplo, `="http://server/site/library/folder/Report1.rdl"`.  
  
## <a name="see-also"></a>Vea también  
 [Agregar una imagen externa &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/add-an-external-image-report-builder-and-ssrs.md)   
 [Agregar un subinforme y parámetros &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/add-a-subreport-and-parameters-report-builder-and-ssrs.md)   
 [Agregar una acción de obtención de detalles en un informe &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md)  
  
  

---
title: Buscar informes y otros elementos (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 6a586659-5c2b-453b-8f40-a3a469277b17
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 36eb4d030933594900d4f73c180fd92cc0323d66
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48145781"
---
# <a name="searching-for-reports-and-other-items-report-builder--and-ssrs"></a>Buscar informes y otros elementos (Generador de informes y SSRS)
  Puede usar el Administrador de informes para buscar en un servidor de informes elementos específicos por nombre o descripción. Tiene la posibilidad de buscar informes publicados, modelos de informe, carpetas, orígenes de datos compartidos y recursos. En cambio, no pueden realizarse búsquedas de programaciones, propietarios, asignaciones de roles, instantáneas específicas del historial del informe ni suscripciones. La búsqueda se realiza en la base de datos del servidor de informes en la que se almacenan los elementos.  
  
> [!NOTE]  
>  La búsqueda en el sistema de archivos no devuelve resultados para los elementos administrados por el servidor de informes.  
  
-   Para buscar elementos en el Administrador de informes, escriba la cadena para buscar en el cuadro de texto **Buscar** que figura en la parte superior de la página. La búsqueda se inicia en el nodo superior de la jerarquía de carpetas y prosigue hacia abajo examinando cada rama. En caso de no tener permiso de acceso a una determinada rama, ésta se omite del proceso. Este comportamiento también es válido para las carpetas Mis informes que pertenecen a otros usuarios y para otras carpetas que no suelen estar disponibles. Los resultados de la búsqueda se limitan exclusivamente a los informes y los elementos para los que el usuario tiene permiso de visualización.  
  
-   Para buscar un elemento por nombre o descripción, especifique una parte del texto que desee que coincida o el texto completo. La cadena para buscar no distingue mayúsculas de minúsculas. Tenga en cuenta que no puede utilizar operadores de búsqueda como los signos más (+) o menos (–) para exigir o excluir criterios de búsqueda.  
  
-   Para buscar texto específico dentro de un informe, use la barra de herramientas situada en la parte superior del informe.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Buscar y ver informes en el Administrador de informes &#40;Generador de informes y SSRS&#41;](finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md)   
 [Usar Mis informes &#40;Generador de informes y SSRS&#41;](using-my-reports-report-builder-and-ssrs.md)   
 [Buscar, ver y administrar informes &#40;Generador de informes y SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Abrir y cerrar un informe &#40;Administrador de informes&#41;](../reports/open-and-close-a-report-report-manager.md)  
  
  

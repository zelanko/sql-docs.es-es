---
title: Solucionar problemas de elementos de informe (generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: d9fe1932-46e7-421b-a8a9-4c54d9576e94
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2aa21825563ae94a46a7d9fcda6e52e966f12a9a
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53360257"
---
# <a name="troubleshoot-report-parts-report-builder-and-ssrs"></a>Solucionar problemas de elementos de informe (Generador de informes y SSRS)
  Estas sugerencias pueden ayudar al trabajar con elementos de informe.  
  
## <a name="why-do-my-co-worker-and-i-see-different-instances-of-the-same-report-part-when-we-search-for-it"></a>¿Por qué mi colaborador y yo vemos instancias diferentes del mismo elemento de informe cuando lo buscamos?  
 Puede haber varias instancias de un elemento de informe único en un servidor de informes o sitio de SharePoint integrado con un servidor de informes, y todas las instancias tendrán el mismo identificador único global (GUID). Solo la instancia más reciente se muestra en la lista de resultados de la búsqueda. En algunas situaciones, las diferentes instancias de un elemento de informe único pueden tener permisos diferentes. Si su colaborador y usted tienen permisos diferentes en el servidor, no verá la misma instancia. Por ejemplo, imagine que varias copias de un elemento de informe, todas con el mismo GUID, están guardadas en distintas carpetas en un servidor de informes en modo integrado de SharePoint. Si las carpetas tienen distintos permisos, los elementos de informe de esas carpetas también tendrán permisos diferentes.  
  
 Para ver qué permisos tienen usted y su colaborador, pregunte al administrador del servidor de informes.  
  
## <a name="when-i-search-for-report-parts-that-i-uploaded-to-a-sharepoint-server-i-do-not-see-them-why-not"></a>Cuando busco elementos de informe que cargué en un servidor de SharePoint, no los veo. ¿Por qué no?  
 Los elementos de informe que ha cargado manualmente en una biblioteca de documentos de SharePoint, en lugar de publicarlos mediante el Generador de informes, podrían no aparecer en la galería de elementos de informe. El servidor de informes utilizado para la búsqueda en la galería podría tener que sincronizarse con el contenido de la biblioteca de documentos de SharePoint. Para obtener más información, consulte [activar la característica de sincronización de archivos de servidor de informes en Administración Central de SharePoint](../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md) en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [libros](https://go.microsoft.com/fwlink/?LinkId=154888) en msdn.microsoft.com.  
  
## <a name="why-cant-others-see-the-image-in-their-reports"></a>¿Por qué otros no pueden ver la imagen en sus informes?  
 Si publica un elemento de informe que es un vínculo a un archivo de imagen, el elemento de informe es en realidad solo un vínculo. Si otros no pueden ver la imagen cuando agregan el elemento de informe de imagen a sus informes, puede que no dispongan de los permisos para la imagen a la que les está vinculando.  
  
 Hay varias soluciones posibles para esto:  
  
-   Convierta el archivo de imagen en un elemento de informe, en lugar de hacer que el vínculo al archivo de imagen sea el elemento de informe.  
  
-   Mueva el archivo de imagen a una ubicación para la que otros tengan permisos.  
  
-   Pida al administrador del servidor de informes que cambie los permisos.  
  
## <a name="why-do-i-get-a-circular-reference-error-message-when-i-try-to-publish-my-report-part"></a>¿Por qué obtengo un mensaje de error de "referencia circular" cuándo intento publicar mi elemento de informe?  
 Si los elementos de informe tienen una referencia circular, no podrá publicarlos como elementos de informe. Por ejemplo, un elemento de informe señala a un conjunto de datos, que a su vez señala a un parámetro. Por último, el parámetro también señala al conjunto de datos. Tendrá que eliminar una de las referencias para poder publicar el elemento de informe.  
  
## <a name="see-also"></a>Vea también  
 [Elementos de informe &#40;Generador de informes y SSRS&#41;](report-parts-report-builder-and-ssrs.md)  
  
  

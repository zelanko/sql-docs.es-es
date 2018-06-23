---
title: Actualizar un recurso (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- updating resources
- resources [Reporting Services], updating
ms.assetid: d21f7493-bcf7-4e9e-9886-55ebdc1f1037
caps.latest.revision: 16
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 012d0a129f97b87423f295f56c3b00e13a542c4e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103041"
---
# <a name="update-a-resource-report-manager"></a>Actualizar un recurso (Administrador de informes)
  Puede actualizar un recurso reemplazándolo por una versión más reciente. Los recursos son elementos almacenados en un servidor de informes que contienen el contenido de un archivo que el usuario carga. Puede reemplazar un recurso existente importando el contenido de archivo nuevo o diferente en el recurso existente. La actualización de un recurso proporciona un modo de actualizar contenido preservando las propiedades existentes y la configuración de seguridad del recurso.  
  
### <a name="to-update-a-resource"></a>Para actualizar un recurso  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  En el Administrador de informes, navegue al recurso que desea actualizar o búsquelo.  
  
3.  Haga clic en el recurso para abrirlo en la página **Vista** .  
  
4.  Haga clic en **Propiedades** para abrir la página de propiedades **General** .  
  
5.  Haga clic en **Reemplazar** para abrir la página de propiedades **Importar recurso** .  
  
6.  Haga clic en **Examinar**.  
  
7.  Seleccione el archivo que desea utilizar para reemplazar el recurso actual. Puede utilizar una versión actualizada del archivo de recursos o especificar un archivo con un nombre o tipo de archivo diferente.  
  
8.  Haga clic en **Aceptar** para cargar el archivo de recursos, cierre la página **Importar recurso** y guarde los cambios en el servidor de informes.  
  
 Si el recurso que está actualizando contiene una imagen que se utiliza en un informe, debe actualizar el informe para ver la imagen actualizada.  
  
## <a name="see-also"></a>Vea también  
 [El contenido de página &#40;el Administrador de informes&#41;](../contents-page-report-manager.md)   
 [Página Cargar archivo &#40;Administrador de informes&#41;](../upload-file-page-report-manager.md)   
 [Carga de archivos a una carpeta](upload-files-to-a-folder.md)   
 [El Administrador de informes (Ayuda F1)](../report-manager-f1-help.md)  
  
  
---
title: Actualización de un recurso (portal web) | Microsoft Docs
description: Actualice un recurso mediante el portal web de Reporting Services. Reemplace un recurso existente mediante la importación de contenido de archivo nuevo o diferente en el recurso existente.
ms.date: 06/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- updating resources
- resources [Reporting Services], updating
ms.assetid: d21f7493-bcf7-4e9e-9886-55ebdc1f1037
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a59d655ef6101d8b9968ff2a241eff7d245ecc75
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547847"
---
# <a name="update-a-resource-web-portal"></a>Actualización de un recurso (portal web)
  Puede actualizar un recurso reemplazándolo por una versión más reciente. Los recursos son elementos almacenados en un servidor de informes que contienen el contenido de un archivo que el usuario carga. Puede reemplazar un recurso existente importando el contenido de archivo nuevo o diferente en el recurso existente. La actualización de un recurso proporciona un modo de actualizar contenido preservando las propiedades existentes y la configuración de seguridad del recurso.  
  
## <a name="to-update-a-resource"></a>Para actualizar un recurso  
  
1.  Inicie [el portal web de un servidor de informes (modo nativo de SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md).  
  
2.  Navegue al recurso que desea actualizar o búsquelo.  
  
3.  Haga clic con el botón derecho en el recurso y seleccione **Administrar** en el menú desplegable.  
  
4.  Seleccione la página **Propiedades** y seleccione **Reemplazar**.  
  
5.  En el cuadro de diálogo **Abrir**, vaya hasta el directorio que contiene el archivo que desea usar como nuevo recurso.  
  
6.  Seleccione el archivo que desea utilizar para reemplazar el recurso actual. Puede utilizar una versión actualizada del archivo de recursos o especificar un archivo con un nombre o tipo de archivo diferente.  
  
7.  Seleccione **Abrir** para cargar el archivo de recursos, y guarde los cambios en el servidor de informes.  
  
 Si el recurso que está actualizando contiene una imagen que se utiliza en un informe, debe actualizar el informe para ver la imagen actualizada.  
  
## <a name="see-also"></a>Consulte también  
 [Administración de contenido del servidor de informes (modo nativo de SSRS)](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Carga de archivos a una carpeta](../../reporting-services/report-server/upload-files-to-a-folder.md)   
  

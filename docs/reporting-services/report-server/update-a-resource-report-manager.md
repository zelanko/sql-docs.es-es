---
title: "Actualizar un recurso (Administrador de informes) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "actualizar recursos"
  - "recursos [Reporting Services], actualizar"
ms.assetid: d21f7493-bcf7-4e9e-9886-55ebdc1f1037
caps.latest.revision: 17
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 17
---
# Actualizar un recurso (Administrador de informes)
  Puede actualizar un recurso reemplazándolo por una versión más reciente. Los recursos son elementos almacenados en un servidor de informes que contienen el contenido de un archivo que el usuario carga. Puede reemplazar un recurso existente importando el contenido de archivo nuevo o diferente en el recurso existente. La actualización de un recurso proporciona un modo de actualizar contenido preservando las propiedades existentes y la configuración de seguridad del recurso.  
  
### Para actualizar un recurso  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md).  
  
2.  En el Administrador de informes, navegue al recurso que desea actualizar o búsquelo.  
  
3.  Haga clic en el recurso para abrirlo en la página **Vista** .  
  
4.  Haga clic en **Propiedades** para abrir la página de propiedades **General** .  
  
5.  Haga clic en **Reemplazar** para abrir la página de propiedades **Importar recurso** .  
  
6.  Haga clic en **Examinar**.  
  
7.  Seleccione el archivo que desea utilizar para reemplazar el recurso actual. Puede utilizar una versión actualizada del archivo de recursos o especificar un archivo con un nombre o tipo de archivo diferente.  
  
8.  Haga clic en **Aceptar** para cargar el archivo de recursos, cierre la página **Importar recurso** y guarde los cambios en el servidor de informes.  
  
 Si el recurso que está actualizando contiene una imagen que se utiliza en un informe, debe actualizar el informe para ver la imagen actualizada.  
  
## Vea también  
 [Contenido &#40;página del Administrador de informes&#41;](../Topic/Contents%20Page%20\(Report%20Manager\).md)   
 [Cargar archivo &#40;página del Administrador de informes&#41;](../Topic/Upload%20File%20Page%20\(Report%20Manager\).md)   
 [Cargar archivos a una carpeta](../../reporting-services/report-server/upload-files-to-a-folder.md)   
 [Administrador de informes (Ayuda F1)](../Topic/Report%20Manager%20F1%20Help.md)  
  
  
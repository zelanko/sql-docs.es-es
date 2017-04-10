---
title: "Cargar un archivo o un informe (Administrador de informes) | Microsoft Docs"
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
  - "publicar informes [Reporting Services], cargar archivos"
  - "informes [Reporting Services], publicar"
  - "cargar informes [Reporting Services]"
  - "cargar archivos [Reporting Services]"
  - "archivos [Reporting Services], cargar"
ms.assetid: 79027e11-f4ba-4bfd-bd8c-d334e3da02a1
caps.latest.revision: 42
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 42
---
# Cargar un archivo o un informe (Administrador de informes)
  El Administrador de informes proporciona una característica de carga para poder agregar informes, modelos y otros archivos a un servidor de informes sin tener que publicar dichos elementos desde una aplicación cliente. Los archivos que se cargan del sistema de archivos se almacenan como elementos en el servidor de informes. El tipo de archivo que se carga determina la manera de almacenarse:  
  
-   Los archivos .rdl se almacenan como informes.  
  
-   Los archivos .smdl se almacenan como modelos de informe.  
  
-   Todos los demás archivos, incluyendo los archivos de origen de datos compartido (.rds), se cargan como recursos. Los recursos no se procesan por un servidor de informes pero se pueden ver en el Administrador de informes si el servidor de informes admite el tipo MIME del archivo.  
  
### Para cargar un archivo o un informe  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md).  
  
2.  En el Administrador de informes, navegue hasta la página **Contenido** . Navegue a la carpeta en la que desea agregar un elemento.  
  
3.  Haga clic en **Cargar archivo**.  
  
4.  Haga clic en **Examinar** para seleccionar el archivo que se va a cargar. Se puede cargar un archivo de definición de informe, una imagen, un documento o cualquier archivo que desee que esté disponible en un servidor de informes.  
  
5.  Escriba el nombre del nuevo elemento. Un nombre de elemento puede incluir espacios, pero no puede incluir caracteres reservados: : @ & = + , $ / * \< > |.  
  
6.  Si desea reemplazar un elemento existente por el nuevo elemento, seleccione **Sobrescribir elemento si existe**.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Vea también  
 [Crear, eliminar o modificar un origen de datos compartido &#40;Administrador de informes&#41;](../Topic/Create,%20Delete,%20or%20Modify%20a%20Shared%20Data%20Source%20\(Report%20Manager\).md)   
 [Contenido &#40;página del Administrador de informes&#41;](../Topic/Contents%20Page%20\(Report%20Manager\).md)   
 [Cargar archivo &#40;página del Administrador de informes&#41;](../Topic/Upload%20File%20Page%20\(Report%20Manager\).md)   
 [Cargar archivos a una carpeta](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
  
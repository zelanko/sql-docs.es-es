---
title: Cargar un archivo o un informe (Administrador de informes) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
ms.assetid: 79027e11-f4ba-4bfd-bd8c-d334e3da02a1
caps.latest.revision: "42"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: c5934844dd9570ab95ab5641d66a465f57725e55
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="upload-a-file-or-report-report-manager"></a>Cargar un archivo o un informe (Administrador de informes)
  El Administrador de informes proporciona una característica de carga para poder agregar informes, modelos y otros archivos a un servidor de informes sin tener que publicar dichos elementos desde una aplicación cliente. Los archivos que se cargan del sistema de archivos se almacenan como elementos en el servidor de informes. El tipo de archivo que se carga determina la manera de almacenarse:  
  
-   Los archivos .rdl se almacenan como informes.  
  
-   Los archivos .smdl se almacenan como modelos de informe.  
  
-   Todos los demás archivos, incluyendo los archivos de origen de datos compartido (.rds), se cargan como recursos. Los recursos no se procesan por un servidor de informes pero se pueden ver en el Administrador de informes si el servidor de informes admite el tipo MIME del archivo.  
  
### <a name="to-upload-a-file-or-report"></a>Para cargar un archivo o un informe  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  En el Administrador de informes, navegue hasta la página **Contenido** . Navegue a la carpeta en la que desea agregar un elemento.  
  
3.  Haga clic en **Cargar archivo**.  
  
4.  Haga clic en **Examinar** para seleccionar el archivo que se va a cargar. Se puede cargar un archivo de definición de informe, una imagen, un documento o cualquier archivo que desee que esté disponible en un servidor de informes.  
  
5.  Escriba el nombre del nuevo elemento. Un nombre de elemento puede incluir espacios, pero no puede incluir caracteres reservados: : @ & = + , $ / * < > |.  
  
6.  Si desea reemplazar un elemento existente por el nuevo elemento, seleccione **Sobrescribir elemento si existe**.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Crear, eliminar o modificar un origen de datos compartido &#40;Administrador de informes&#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)   
 [Contenido &#40;página del Administrador de informes&#41;](http://msdn.microsoft.com/library/6b16869b-158a-4934-9c85-bee934b35378)   
 [Página Cargar archivo &#40;Administrador de informes&#41;](http://msdn.microsoft.com/library/7bb3166f-9374-4449-b66a-ffb77298507d)   
 [Carga de archivos a una carpeta](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
  

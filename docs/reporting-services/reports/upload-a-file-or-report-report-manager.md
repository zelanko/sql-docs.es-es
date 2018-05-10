---
title: Cargar un archivo o un informe (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: reports
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
ms.assetid: 79027e11-f4ba-4bfd-bd8c-d334e3da02a1
caps.latest.revision: 42
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d5485f3c29c394655371ff42b690ccbacdcdd53d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
  
## <a name="see-also"></a>Ver también  
 [Crear, eliminar o modificar un origen de datos compartido &#40;Administrador de informes&#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)   
 [Contenido &#40;página del Administrador de informes&#41;](http://msdn.microsoft.com/library/6b16869b-158a-4934-9c85-bee934b35378)   
 [Página Cargar archivo &#40;Administrador de informes&#41;](http://msdn.microsoft.com/library/7bb3166f-9374-4449-b66a-ffb77298507d)   
 [Carga de archivos a una carpeta](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
  

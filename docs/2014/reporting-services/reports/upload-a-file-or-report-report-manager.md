---
title: Cargar un archivo o un informe (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
ms.assetid: 79027e11-f4ba-4bfd-bd8c-d334e3da02a1
caps.latest.revision: 41
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 44dd1787da648e332c2234b83323990784b0d4bc
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39085447"
---
# <a name="upload-a-file-or-report-report-manager"></a>Cargar un archivo o un informe (Administrador de informes)
  El Administrador de informes proporciona una característica de carga para poder agregar informes, modelos y otros archivos a un servidor de informes sin tener que publicar dichos elementos desde una aplicación cliente. Los archivos que se cargan del sistema de archivos se almacenan como elementos en el servidor de informes. El tipo de archivo que se carga determina la manera de almacenarse:  
  
-   Los archivos .rdl se almacenan como informes.  
  
-   Los archivos .smdl se almacenan como modelos de informe.  
  
-   Todos los demás archivos, incluyendo los archivos de origen de datos compartido (.rds), se cargan como recursos. Los recursos no se procesan por un servidor de informes pero se pueden ver en el Administrador de informes si el servidor de informes admite el tipo MIME del archivo.  
  
### <a name="to-upload-a-file-or-report"></a>Para cargar un archivo o un informe  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  En el Administrador de informes, navegue hasta la página **Contenido** . Navegue a la carpeta en la que desea agregar un elemento.  
  
3.  Haga clic en **Cargar archivo**.  
  
4.  Haga clic en **Examinar** para seleccionar el archivo que se va a cargar. Se puede cargar un archivo de definición de informe, una imagen, un documento o cualquier archivo que desee que esté disponible en un servidor de informes.  
  
5.  Escriba el nombre del nuevo elemento. Un nombre de elemento puede incluir espacios, pero no puede incluir caracteres reservados: : \@ & = +, $ / * \< > |.  
  
6.  Si desea reemplazar un elemento existente por el nuevo elemento, seleccione **Sobrescribir elemento si existe**.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Crear, eliminar o modificar un origen de datos compartido &#40;el Administrador de informes&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [El contenido de página &#40;el Administrador de informes&#41;](../contents-page-report-manager.md)   
 [Página Cargar archivo &#40;Administrador de informes&#41;](../upload-file-page-report-manager.md)   
 [Carga de archivos a una carpeta](../report-server/upload-files-to-a-folder.md)  
  
  

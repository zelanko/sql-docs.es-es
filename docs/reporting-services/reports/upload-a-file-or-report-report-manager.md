---
title: Cargar un archivo o un informe en el servidor de informes | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2018
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
ms.openlocfilehash: 1f0406d711dfb04e553cb7ba8f8c27ede209a5f2
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34550106"
---
# <a name="upload-a-file-or-report-in-the-report-server"></a>Cargar un archivo o un informe en el servidor de informes
En el portal web del servidor de informes se proporciona una característica de carga para poder agregar informes y otros archivos a un servidor de informes sin tener que publicar esos elementos desde una aplicación cliente. Los archivos que se cargan del sistema de archivos se almacenan como elementos en el servidor de informes. El tipo de archivo que se carga determina la manera de almacenarse:  
  
-   Los archivos .rdl se almacenan como informes paginados.  
  
-   Todos los demás archivos, incluyendo los archivos de origen de datos compartido (.rds), se cargan como recursos. Los recursos no son procesados por un servidor de informes, pero pueden verse en el portal web si el servidor de informes admite el tipo MIME del archivo.  
  
### <a name="to-upload-a-file-or-report"></a>Para cargar un archivo o un informe  
  
1.  En el portal web, haga clic en **Cargar**.  
  
4.  Busque el archivo que quiera cargar. Se puede cargar un archivo de definición de informe, una imagen, un documento o cualquier archivo que desee que esté disponible en un servidor de informes.  
  
5.  Escriba el nombre del nuevo elemento. Un nombre de elemento puede incluir espacios, pero no puede incluir caracteres reservados: : @ & = + , $ / * < > |.  
  
6.  Si desea reemplazar un elemento existente por el nuevo elemento, seleccione **Sobrescribir elemento si existe**.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Ver también   
[Crear, modificar y eliminar orígenes de datos compartidos](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)
[Cargar archivos a una carpeta](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
  

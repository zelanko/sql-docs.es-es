---
title: Cargar archivos a una carpeta | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
- files [Reporting Services]
- folders [Reporting Services], uploading files to
ms.assetid: 2f99a288-d4aa-4c64-b310-e457a2aef2c5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9b0d32e2705b63ddc5f12af84e0589a9c940582d
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2018
ms.locfileid: "50029684"
---
# <a name="upload-files-to-a-folder"></a>Cargar archivos a una carpeta
  Puede cargar archivos desde el sistema de archivos y almacenarlos en una base de datos del servidor de informes como elementos administrados. Lo que sucede al cargar el archivo depende del tipo de archivo.  
  
-   Cargar un archivo .rdl equivale a publicar un informe.  
  
-   Al cargar cualquier otro tipo de archivo, éste se agrega a la base de datos del servidor de informes como un objeto binario único. Estos archivos se publican en un servidor de informes como recurso. Los recursos pueden ser cualquier tipo de archivo. Si la extensión de archivo corresponde a la de un tipo MIME conocido, se utilizará un icono de dicho tipo MIME para identificar el tipo de recurso. De lo contrario, los recursos se indican mediante un icono de archivo genérico.  
  
> [!NOTE]  
>  No se pueden cargar archivos de origen de datos de informes (.rds) para crear un origen de datos compartido. Los archivos .rds solo se utilizan en el Diseñador de informes. No puede proporcionar el contenido para un elemento de origen de datos compartido que se defina y administre mediante el Administrador de informes. Como alternativa a la carga, se puede escribir un script que cree un origen de datos compartido basado en un archivo .rds.  
  
 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]determina el tamaño de archivo máximo para los elementos cargados. De manera predeterminada, el tamaño máximo es de 4 megabytes (MB).  
  
 Visualmente, los archivos que se cargan a la base de datos del servidor de informes aparecen representados en la jerarquía de carpetas con los siguientes iconos.  
  
 ![Icono de informe](../../reporting-services/report-server/media/hlp-16doc.gif "Icono de informe")  
Icono de informe  
  
 ![Icono de modelo](../../reporting-services/report-server/media/model-icon.gif "Icono de modelo")  
Icono de modelo de informe  
  
 ![Icono de recurso genérico](../../reporting-services/report-server/media/hlp-16file.gif "Icono de recurso genérico")  
Icono de recurso genérico  
  
 Al cargar un archivo, éste se sitúa siempre en la carpeta seleccionada. Puede navegar en primer lugar hasta la carpeta en la que desea hospedar el elemento o bien puede cargar el archivo y moverlo después a la ubicación final.  
  
 Para cargar un archivo, use el Administrador de informes. Podrá cargar archivos a un servidor de informes dependiendo de qué tareas formen parte de su asignación de roles. Si utiliza la seguridad predeterminada, solo los administradores locales podrán agregar elementos a un servidor de informes. Si está habilitado el rol Mis informes, cada usuario que disponga de una carpeta Mis informes tendrá permiso para cargar archivos a esa carpeta. Si utiliza asignaciones de roles personalizados, deberán incluir las tareas compatibles con la administración de carpetas.  
  
|Para|Incluya estas tareas|  
|----------------|-------------------------|  
|Cargar un archivo .rdl a una carpeta|Administrar informes|  
|Cargar cualquier archivo como objeto binario|Administrar recursos|  
|Ver el contenido de una carpeta|Ver recursos, Ver informes|  
  
## <a name="see-also"></a>Ver también  
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Conceder permisos en un servidor de informes en modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Tareas y permisos](../../reporting-services/security/tasks-and-permissions.md)   
 [Cargar un archivo o un informe &#40;Administrador de informes&#41;](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)  
  
  

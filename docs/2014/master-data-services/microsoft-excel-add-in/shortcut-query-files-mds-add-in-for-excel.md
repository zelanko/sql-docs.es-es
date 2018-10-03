---
title: Archivos de consulta de acceso directo (complemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: 1ba0219a-6c40-41fa-aff9-8c8f41ef3220
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: e49af33f5e7c02536757cf408e9b774852a9002b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48215665"
---
# <a name="shortcut-query-files-mds-add-in-for-excel"></a>Archivos de consulta de acceso directo (complemento MDS para Excel)
  En el [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], puede usar los archivos de consulta de acceso directo para conectarse a datos usados con frecuencia y cargarlos rápidamente. También puede utilizarlos si desea compartir datos MDS con otros. En lugar de guardar la hoja de cálculo y enviarla por correo electrónico, debe guardar un archivo de consulta de acceso directo y enviarlo por correo electrónico. Esto garantiza que ambos se conecten al repositorio MDS para obtener los datos más recientes.  
  
 Los archivos de consulta de acceso directo son archivos XML que contienen información acerca de:  
  
-   La conexión del repositorio MDS.  
  
-   El modelo, versión y entidad.  
  
-   Los filtros que se aplicaron cuando se creó el acceso directo.  
  
-   El orden de izquierda a derecha de las columnas cuando se creó el acceso directo.  
  
 Puede guardar los archivos en una lista y elegir entre ellos cuando abra el complemento. Puede exportarlos al equipo o a una ubicación compartida, o puede enviarlos a otros.  
  
## <a name="queryopener-application"></a>Aplicación QueryOpener  
 Todos los usuarios que instalan [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] tienen instalada una aplicación denominada QueryOpener. Esta aplicación se usa para abrir los archivos de consulta de acceso directo en [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]. Si hace doble clic en un archivo de consulta de acceso directo, esta aplicación se usa automáticamente para abrir el archivo en el complemento.  
  
 Cuando se abre un archivo de consulta de acceso directo con esta aplicación, se le pedirá que realice una conexión 'segura', lo que significa que confía en el contenido de esta ubicación. Cada vez que se marca una conexión como segura, se agrega a una lista. Si desea desactivar esta lista, abra el cuadro de diálogo **Configuración** y, en la sección **Servidores agregados a la lista segura** , haga clic en **Borrar todo**.  
  
 La ubicación predeterminada para la aplicación es *unidad*: \Program Files\Microsoft SQL Server\120\Master Data Services\Excel Add-In\Microsoft.MasterDataServices.QueryOpener.exe.  
  
 Hay dos maneras de abrir los archivos de consulta de acceso directo: puede importarlos o puede hacer doble clic en ellos para que se abran automáticamente.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Guardar el contenido de la hoja de cálculo activa como un archivo de consulta de acceso directo.|[Guardar un archivo de consulta de acceso directo &#40;complemento MDS para Excel&#41;](save-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|Enviar por correo electrónico un archivo de consulta de acceso directo que representa el contenido de la hoja de cálculo activa.|[Enviar por correo electrónico un archivo de consulta de acceso directo &#40;complemento MDS para Excel&#41;](email-a-shortcut-query-file-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Conexiones &#40;complemento MDS para Excel&#41;](connections-mds-add-in-for-excel.md)  
  
-   [Complemento de Master Data Services para Microsoft Excel](master-data-services-add-in-for-microsoft-excel.md)  
  
-   [Seguridad &#40;Master Data Services&#41;](../security-master-data-services.md)  
  
  

---
title: Particiones (cuadro de diálogo restaurar base de datos) (Analysis Services-datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.restoredbdialog.partitions.f1
ms.assetid: 1ad4dde5-4651-4069-875c-7ab73cd8b4f4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a0c28420d711fd009dfc2b1e36ef4a613b3ecfaf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66072112"
---
# <a name="partitions-restore-database-dialog-box-analysis-services---multidimensional-data"></a>Particiones (cuadro de diálogo Restaurar base de datos) (Analysis Services - Datos multidimensionales)
  Utilice la página **Particiones** del cuadro de diálogo **Restaurar base de datos** de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para especificar la ubicación en la que se restaurarán las particiones locales y si es necesario restaurar particiones remotas, así como los archivos de copia de seguridad remotos que se utilizarán al restaurar las particiones remotas.  
  
> [!IMPORTANT]  
>  Para cada archivo de copia de seguridad, el usuario que ejecuta el comando de restauración debe tener permiso para leer desde la ubicación de la copia de seguridad especificada. Para restaurar una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que no está instalada en el servidor, el usuario también debe ser miembro del rol de servidor para dicha instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Para sobrescribir una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , el usuario debe tener uno de los roles siguientes: miembro del rol de servidor para la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o miembro de un rol de base de datos con permisos de Control total (Administrador) en la base de datos que se va a restaurar.  
  
> [!NOTE]  
>  Después de restaurar una base de datos existente, el usuario que restauró la base de datos podría perder el acceso a la base de datos restaurada. Esta pérdida de acceso puede producirse si, en el momento en que se realizó la copia de seguridad, el usuario no era miembro del rol de servidor o no era miembro de rol de base de datos con permisos de Control total (Administrador).  
  
 **Para mostrar la página particiones en el cuadro de diálogo restaurar base de datos**  
  
-   En [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], haga clic con el botón derecho en la carpeta **Bases de datos** de una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o en una base de datos en el **Explorador de objetos**, haga clic en **Restaurar**y, después, en **Seleccionar una página**, haga clic en **Particiones**.  
  
## <a name="options"></a>Opciones  
 **Script**  
 Crea un script de restauración basado en las opciones seleccionadas en el cuadro de diálogo. El script de restauración se escribe en el lenguaje de scripting de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] (ASSL).  
  
 Al hacer clic en el icono **Script** , se envía el script de restauración a una nueva ventana de consulta, de forma predeterminada.  
  
 Al hacer clic en la flecha **Script** , se muestra un menú que le permite elegir dónde enviar el script de restauración:  
  
-   A una nueva ventana de consulta (predeterminada)  
  
-   A un archivo  
  
-   Al Portapapeles  
  
-   A un trabajo  
  
 **Restaurar a ubicaciones originales**  
 Seleccione esta opción para restaurar las particiones locales incluidas en el archivo de copia de seguridad a sus ubicaciones originales.  
  
 **Seleccionar ubicaciones diferentes**  
 Seleccione esta opción para especificar ubicaciones diferentes en las que se restaurarán las particiones locales.  
  
> [!NOTE]  
>  Solo puede cambiar la carpeta de restauración de una partición local si en el cubo se especificó una ubicación distinta de la ubicación predeterminada para esa partición.  
  
 La siguiente cuadrícula, que se habilita cuando se selecciona esta opción, se utiliza para especificar una carpeta de restauración para cada partición local:  
  
|Columna|Descripción|  
|------------|-----------------|  
|**BD**|Muestra el nombre del cubo que contiene la partición local.|  
|**MeasureGroup**|Muestra el nombre del grupo de medida que contiene la partición local.|  
|**Divide**|Muestra el nombre de la partición local.|  
|**Tamaño (MB)**|Muestra el tamaño de la partición local en megabytes.|  
|**Carpeta original**|Muestra el nombre de la carpeta original en la que se almacenó la partición local.|  
|**Carpeta de restauración**|Escriba el nombre de la carpeta de restauración de la partición local, o bien haga clic en el botón de puntos suspensivos (**…**) para mostrar el cuadro de diálogo **Buscar carpeta remota** y seleccione la ruta de acceso a la carpeta que quiera usar. Para obtener más información sobre el cuadro de diálogo **Buscar carpeta remota**, vea [Cuadro de diálogo Buscar carpeta remota &#40;Analysis Services - Datos multidimensionales&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md).|  
  
 **Restaurar particiones remotas**  
 Seleccione esta opción para restaurar particiones remotas almacenadas en archivos de copia de seguridad remotos.  
  
> [!NOTE]  
>  Esta opción solo se habilita si el archivo de copia de seguridad contiene referencias a las particiones remotas.  
  
 La siguiente cuadrícula, que se habilita cuando se selecciona esta opción, se utiliza para especificar una carpeta de restauración para cada partición local:  
  
|Columna|Descripción|  
|------------|-----------------|  
|**Server**|Muestra el nombre de la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que administra la partición remota.|  
|**Data Source** (Origen de datos)|Muestra el nombre del origen de datos del archivo de copia de seguridad que representa la base de datos que contiene la partición remota.|  
|**Archivo de copia de seguridad**|Escriba la ruta de acceso completa y el nombre de archivo del archivo de copia de seguridad remoto que quiere usar, o bien haga clic en el botón de puntos suspensivos (**…**) para mostrar el cuadro de diálogo **Buscar archivos de la base de datos** y seleccionar la ruta de acceso y el nombre de archivo del archivo de copia de seguridad remoto que quiere usar. Para más información sobre el cuadro de diálogo **Buscar archivos de base de datos**, vea [Cuadro de diálogo Buscar archivos de la base de datos &#40;Analysis Services - Datos multidimensionales&#41;](locate-database-files-dialog-box-analysis-services-multidimensional-data.md).|  
|**...**|Haga clic en este botón para mostrar el cuadro de diálogo **Particiones remotas - Configuración avanzada** y modificar opciones avanzadas, como la cadena de conexión del origen de datos, para restaurar la partición remota. Para más información sobre el cuadro de diálogo **Particiones remotas - Configuración avanzada**, vea [Cuadro de diálogo Particiones remotas: configuración avanzada &#40;Analysis Services - Datos multidimensionales&#41;](remote-partitions-advanced-settings-dialog-analysis-services-multidimensional-data.md).|  
  
## <a name="see-also"></a>Consulte también  
 [Cuadro de diálogo restaurar base de datos &#40;Analysis Services-datos multidimensionales&#41;](restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Cuadro de diálogo restaurar base de datos de &#40;general&#41; &#40;Analysis Services de datos multidimensionales&#41;](general-restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Realizar una copia de seguridad y restaurar las bases de datos de Analysis Services](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  

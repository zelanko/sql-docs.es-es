---
title: Cuadro de diálogo copia de seguridad de base de datos (Analysis Services-datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.Backup.f1
ms.assetid: 7811ce7d-6c37-4189-bfa6-ef36fb4932db
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a99ce67c4b42cc1def10127c8b1862a859d20723
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66064380"
---
# <a name="backup-database-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Copia de seguridad de la base de datos (Analysis Services - Datos multidimensionales)
  Use el cuadro de diálogo **Copia de seguridad de la base de datos** de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para hacer una copia de seguridad de una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en un archivo de copia de seguridad con el formato de copia de seguridad de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] (.abf).  
  
> [!IMPORTANT]  
>  Para cada archivo de copia de seguridad, el usuario que ejecuta el comando de copia de seguridad debe tener permiso para escribir en la ubicación de copia de seguridad especificada. Además, el usuario debe tener uno de los roles siguientes: miembro de un rol de servidor para la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o miembro de un rol de base de datos con permisos de Control total (Administrador) en la base de datos de la que se va a hacer una copia de seguridad.  
  
 **Para mostrar el cuadro de diálogo Copia de seguridad de la base de datos**  
  
-   En [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], haga clic con el botón derecho en la carpeta **Bases de datos** de una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o en una base de datos del **Explorador de objetos**y, a continuación, haga clic en **Copia de seguridad**.  
  
## <a name="options"></a>Opciones  
 **Script**  
 Crea un script de copia de seguridad basado en las opciones seleccionadas en el cuadro de diálogo. El script de restauración se escribe en el lenguaje de scripting de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] (ASSL).  
  
 Al hacer clic en el icono **Script** , se envía el script de copia de seguridad a una nueva ventana de consulta, de forma predeterminada.  
  
 Al hacer clic en la flecha **Script** , se muestra un menú que permite elegir dónde enviar el script de copia de seguridad:  
  
-   A una nueva ventana de consulta (predeterminada)  
  
-   A un archivo  
  
-   Al Portapapeles  
  
-   A un trabajo  
  
 **Base de datos**  
 Muestra el nombre de la base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] seleccionada.  
  
 **Archivo de copia de seguridad**  
 Escriba la ruta de acceso completa y el nombre del archivo de copia de seguridad que desea utilizar.  
  
 **Examinar**  
 Haga clic para mostrar el cuadro de diálogo **Guardar archivo como** y seleccione la ruta de acceso y el nombre del archivo de copia de seguridad que quiere usar. Para obtener más información sobre el cuadro de diálogo **Guardar archivo como**, vea [Cuadro de diálogo Guardar archivo como &#40;Analysis Services - Datos multidimensionales&#41;](save-file-as-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Permitir la sobrescritura de archivos**  
 Seleccione esta opción para sobrescribir un archivo de copia de seguridad existente o un archivo de copia de seguridad remoto, si existiese.  
  
> [!NOTE]  
>  Si no selecciona esta opción y existe el archivo de seguridad especificado en **Archivo de copia de seguridad** o el archivo de copia de seguridad remoto en **Archivo de copia de seguridad remoto**, se producirá un error.  
  
 **Aplicar compresión**  
 Seleccione esta opción para comprimir el contenido de un archivo de copia de seguridad o los archivos de copia de seguridad remotos especificados.  
  
 **Cifrar archivo de copia de seguridad**  
 Seleccione esta opción para cifrar el archivo de copia de seguridad con la contraseña proporcionada en **Contraseña**.  
  
 **Contraseña**  
 Escriba la contraseña que desea utilizar para cifrar el archivo de copia de seguridad o los archivos de copia de seguridad remotos especificados.  
  
> [!NOTE]  
>   Esta opción solo se habilita si se selecciona **Cifrar archivo de copia de seguridad** .  
  
 **Confirm Password**  
 Escriba la contraseña proporcionada en **Contraseña** para confirmar la contraseña del archivo de copia de seguridad y los archivos de copia de seguridad remotos especificados.  
  
> [!NOTE]  
>   Esta opción solo se habilita si se selecciona **Cifrar archivo de copia de seguridad** .  
  
 **Copia de seguridad de particiones remotas**  
 Seleccione esta opción para incluir información y datos de la ubicación para las particiones remotas del archivo de copia de seguridad.  
  
> [!NOTE]  
>  Esta opción solo se habilita si la base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] seleccionada usa particiones remotas.  
  
 **Ubicación de la copia de seguridad de la partición remota**  
 Muestra la ubicación de las particiones remotas asociadas a la base de datos seleccionada, así como el archivo de copia de seguridad remoto usado para hacer una copia de seguridad de los datos y metadatos de las particiones remotas. Están disponibles las siguientes columnas:  
  
|Columna|Descripción|  
|------------|-----------------|  
|**Server**|Muestra la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que administra las particiones remotas.|  
|**Base de datos**|Muestra la base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que contiene las particiones remotas.|  
|**Lista de particiones**|Muestra la lista de particiones remotas contenidas en la base de datos que se muestra en **Base de datos**.|  
|**Archivo de copia de seguridad remoto**|Escriba la ruta de acceso completa y el nombre del archivo de copia de seguridad remoto que quiere usar o haga clic en el botón de puntos suspensivos (**…**) para mostrar el cuadro de diálogo **Guardar archivo como** y seleccione la ruta de acceso y el nombre del archivo de copia de seguridad remoto que quiere usar. Para obtener más información sobre el cuadro de diálogo **Guardar archivo como**, vea [Cuadro de diálogo Guardar archivo como &#40;Analysis Services - Datos multidimensionales&#41;](save-file-as-dialog-box-analysis-services-multidimensional-data.md).|  
  
## <a name="see-also"></a>Consulte también  
 [Analysis Services diseñadores y cuadros de diálogo &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Realizar una copia de seguridad y restaurar las bases de datos de Analysis Services](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  

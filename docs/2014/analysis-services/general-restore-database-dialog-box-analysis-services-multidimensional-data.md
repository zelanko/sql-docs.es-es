---
title: General (cuadro de diálogo Restaurar base de datos) (Analysis Services - datos multidimensionales) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.restoredbdialog.f1
ms.assetid: 319e7ef5-c9c7-4e50-8690-02a90aed006f
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4969ceb840f6c3d80b4d0854d582e695c109806b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199246"
---
# <a name="general-restore-database-dialog-box-analysis-services---multidimensional-data"></a>General (cuadro de diálogo Restaurar base de datos) (Analysis Services - Datos multidimensionales)
  Use la página **General** del cuadro de diálogo **Restaurar base de datos** en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para especificar el archivo de copia de seguridad y la configuración general que se utilizará al restaurar una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Para cada archivo de copia de seguridad, el usuario que ejecuta el comando de restauración debe tener permiso para leer desde la ubicación de la copia de seguridad especificada. Para restaurar una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que no está instalada en el servidor, el usuario también debe ser miembro del rol de servidor para dicha instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Para sobrescribir una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , el usuario debe tener uno de los roles siguientes: miembro del rol de servidor para la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o miembro de un rol de base de datos con permisos de Control total (Administrador) en la base de datos que se va a restaurar.  
  
> [!NOTE]  
>  Después de restaurar una base de datos existente, el usuario que restauró la base de datos podría perder el acceso a la base de datos restaurada. Esta pérdida de acceso puede producirse si, en el momento en que se realizó la copia de seguridad, el usuario no era miembro del rol de servidor o no era miembro de rol de base de datos con permisos de Control total (Administrador).  
  
 **Para mostrar la página General en el cuadro de diálogo Restaurar base de datos**  
  
-   En [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], haga clic con el botón derecho o en la carpeta **Bases de datos** de una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o en una base de datos en el **Explorador de objetos**, haga clic en **Restaurar**y, luego, en **Seleccionar una página**, haga clic en **General**.  
  
## <a name="options"></a>Opciones  
 **Script**  
 Crea un script de restauración basado en las opciones seleccionadas en el cuadro de diálogo. El script de restauración se escribe en el lenguaje de scripting de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] (ASSL).  
  
 Al hacer clic en el icono **Script** , se envía el script de restauración a una nueva ventana de consulta, de forma predeterminada.  
  
 Al hacer clic en la flecha **Script** , se muestra un menú que le permite elegir dónde enviar el script de restauración:  
  
-   A una nueva ventana de consulta (predeterminada)  
  
-   A un archivo  
  
-   Al Portapapeles  
  
-   A un trabajo  
  
 **Restaurar base de datos**  
 Seleccione la base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que se restaurará.  
  
 **Desde el archivo de copia de seguridad**  
 Seleccione el archivo de copia de seguridad a partir del que se restaurará la base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] seleccionada.  
  
 **Examinar**  
 Haga clic para mostrar el cuadro de diálogo **Buscar archivos de base de datos** y seleccione la ruta de acceso y el nombre del archivo de copia de seguridad que se usará. Para más información sobre el cuadro de diálogo **Buscar archivos de base de datos**, vea [Cuadro de diálogo Buscar archivos de la base de datos &#40;Analysis Services - Datos multidimensionales&#41;](locate-database-files-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Permitir sobrescritura de base de datos**  
 Seleccione esta opción para permitir a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] restaurar el contenido del archivo de copia de seguridad seleccionado sobre objetos existentes en la base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] seleccionada.  
  
 **Incluir información de seguridad**  
 Seleccione esta opción para copiar la información de seguridad almacenada en el archivo de copia de seguridad en la base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 Si esta opción está seleccionada, puede elegir la cantidad de información de seguridad de la lista desplegable habilitada al seleccionar esta opción. Las siguientes opciones están disponibles:  
  
|Opción|Descripción|  
|------------|-----------------|  
|**Copiar todo**|Restaura los roles de base de datos que contiene el archivo de copia de seguridad y también las cuentas de usuario asociadas a los roles.|  
|**Omitir pertenencia**|Restaura los roles de base de datos que contiene el archivo de copia de seguridad, pero no restaura las cuentas de usuario asociadas a los roles.|  
  
 **Contraseña**  
 Si el archivo de copia de seguridad está cifrado, escriba la contraseña usada para cifrarlo.  
  
## <a name="see-also"></a>Vea también  
 [Restaurar base de datos cuadro de diálogo &#40;Analysis Services - datos multidimensionales&#41;](restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Las particiones &#40;restaurar la base de datos cuadro de diálogo&#41; &#40;Analysis Services - datos multidimensionales&#41;](partitions-restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Realizar una copia de seguridad y restaurar las bases de datos de Analysis Services](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
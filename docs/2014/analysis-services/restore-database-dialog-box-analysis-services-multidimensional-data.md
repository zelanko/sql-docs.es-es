---
title: Cuadro de diálogo de la base de datos (Analysis Services - datos multidimensionales) restaurar | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.Restore.f1
ms.assetid: a3990d47-55e2-424e-8eac-87edc937e806
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9231189bb3bf127c7413a0b5d55ae286a32f42cc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748417"
---
# <a name="restore-database-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Restaurar base de datos (Analysis Services - Datos multidimensionales)
  Use el cuadro de diálogo **Restaurar base de datos** de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para restaurar una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] desde un archivo de copia de seguridad con el formato de copia de seguridad de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] (.abf).  
  
> [!IMPORTANT]  
>  Para cada archivo de copia de seguridad, el usuario que ejecuta el comando de restauración debe tener permiso para leer desde la ubicación de la copia de seguridad especificada. Para restaurar una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que no está instalada en el servidor, el usuario también debe ser miembro del rol de servidor para dicha instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Para sobrescribir una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , el usuario debe tener uno de los roles siguientes: miembro del rol de servidor para la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o miembro de un rol de base de datos con permisos de Control total (Administrador) en la base de datos que se va a restaurar.  
  
> [!NOTE]  
>  Después de restaurar una base de datos existente, el usuario que restauró la base de datos podría perder el acceso a la base de datos restaurada. Esta pérdida de acceso puede producirse si, en el momento en que se realizó la copia de seguridad, el usuario no era miembro del rol de servidor o no era miembro de rol de base de datos con permisos de Control total (Administrador).  
  
 **Para mostrar el cuadro de diálogo Restaurar base de datos**  
  
-   En [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], haga clic con el botón derecho en la carpeta **Bases de datos** de una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o en una base de datos en el **Explorador de objetos**y, después, haga clic en **Restaurar**.  
  
 El cuadro de diálogo **Restaurar base de datos** muestra las páginas siguientes.  
  
## <a name="pages"></a>Páginas  
 **General**  
 Use esta página para seleccionar la base de datos que desea restaurar, el archivo de copia de seguridad desde el que desea restaurar la base de datos y las opciones generales y la contraseña para restaurar la base de datos. Para obtener más información sobre esta página, vea [General &#40;cuadro de diálogo Restaurar base de datos&#41; &#40;Analysis Services - Datos multidimensionales&#41;](general-restore-database-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Particiones**  
 Use esta página para restaurar las particiones locales en ubicaciones específicas y para restaurar particiones remotas desde archivos de copia de seguridad remotos. Para obtener más información sobre esta página, vea [Particiones &#40;cuadro de diálogo Restaurar base de datos&#41; &#40;Analysis Services - Datos multidimensionales&#41;](partitions-restore-database-dialog-box-analysis-services-multidimensional-data.md).  
  
## <a name="see-also"></a>Vea también  
 [Diseñadores y cuadros de diálogo de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Realizar una copia de seguridad y restaurar las bases de datos de Analysis Services](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  

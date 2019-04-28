---
title: Opciones de copia de seguridad | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [Analysis Services]
- databases [Analysis Services], backing up
ms.assetid: 02d33fc9-f3f4-4b85-8b90-449b68625cf7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5047647ef5f440987b4b20db99ad42dacf4fc4d0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62727009"
---
# <a name="backup-options"></a>Opciones de copia de seguridad
  Existen varias formas de hacer una copia de seguridad de las bases de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , pero todas ellas tienen en común la necesidad de disponer de permisos de administrador de servidor y administrador de base de datos. Puede abrir el cuadro de diálogo **Copia de seguridad** en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], seleccionar las opciones adecuadas y, a continuación, ejecutar la copia de seguridad desde el mismo cuadro de diálogo. También puede crear un script mediante la configuración que ya está especificada en el archivo. A continuación, el script puede guardarse y ejecutarse siempre que sea necesario.  
  
## <a name="backup-and-synchronize"></a>Hacer una copia de seguridad y sincronizar  
 Si la base de datos reside en una instancia remota de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], puede utilizar la característica de sincronización para realizar una copia de seguridad de la base de datos en la instancia local. Las compilaciones de desarrollo de una base de datos pueden aplicarse a un entorno de producción de esta manera. También puede utilizarse el mecanismo convencional de copias de seguridad y restauración basadas en archivos para trasladar la compilación de desarrollo a un entorno de producción, pero la sincronización proporciona funcionalidad adicional. Por ejemplo, puede establecer una configuración de seguridad diferente para los equipos de desarrollo y de producción. La sincronización le ofrecerá la opción de mantener esa configuración y sincronizar todos los objetos que no son roles. Asimismo, la sincronización realiza normalmente una actualización incremental de los objetos que son diferentes en los equipos origen y destino. La copia de seguridad incremental no está disponible cuando se utiliza la característica de copia de seguridad/restauración. Para más información, consulte [Synchronize Analysis Services Databases](synchronize-analysis-services-databases.md).  
  
> [!IMPORTANT]  
>  La cuenta de servicio de Analysis Services debe tener permiso para escribir en la ubicación de copia de seguridad especificada para cada archivo. Además, el usuario debe tener uno de los roles siguientes: rol de administrador en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o ser miembro de un rol de base de datos con permisos de Control total (Administrador) en la base de datos de la que se va a hacer copia de seguridad.  
  
## <a name="see-also"></a>Vea también  
 [Cuadro de diálogo Copia de seguridad de la base de datos &#40;Analysis Services - Datos multidimensionales&#41;](../backup-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Realizar una copia de seguridad y restaurar las bases de datos de Analysis Services](backup-and-restore-of-analysis-services-databases.md)   
 [Elemento de copia de seguridad &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)   
 [Restaurar, sincronizar y realizar copias de seguridad de bases de datos &#40;XMLA&#41;](../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  

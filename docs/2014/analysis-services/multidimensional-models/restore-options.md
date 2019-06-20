---
title: Opciones de restauración | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], restoring
- restoring databases [Analysis Services]
ms.assetid: 75c73802-f321-4671-afc7-54505d62c013
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a754ac9650c94511e8576a8a05e0b81fb38138a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073084"
---
# <a name="restore-options"></a>Opciones de restauración
  Existen muchas formas de restaurar las bases de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pero todas ellas requieren que tenga permisos de administrador para el equipo servidor y para la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para restaurar una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , puede abrir el cuadro de diálogo **Restaurar base de datos** de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], seleccionar la configuración adecuada de las opciones y, a continuación, ejecutar la restauración desde el cuadro de diálogo. O bien, puede crear un script que utilice los valores ya especificados en el archivo; así podrá guardar el script y ejecutarlo tan a menudo como sea necesario. De esta forma, la restauración se lleva a cabo mediante XMLA, como se describe en la siguiente sección.  
  
## <a name="restoring-databases-using-xmla"></a>Restaurar bases de datos mediante XMLA  
 El comando Restore de XMLA es una forma de automatizar el proceso de restauración ejecutando una restauración basada en un archivo .abf. El comando Restore tiene un número de propiedades que se pueden establecer para especificar definiciones de seguridad, en las que deberían almacenarse las particiones remotas, y la reubicación de objetos OLAP relacionales (ROLAP). Para obtener más información, vea [Restore Element &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla).  
  
> [!IMPORTANT]  
>  Para cada archivo de copia de seguridad, el usuario que ejecuta el comando de restauración debe tener permiso para leer desde la ubicación de la copia de seguridad especificada. Para restaurar una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que no está instalada en el servidor, el usuario también debe ser miembro del rol de servidor para dicha instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para sobrescribir una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , el usuario debe tener uno de los roles siguientes: miembro del rol de servidor para la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o miembro de un rol de base de datos con permisos de Control total (Administrador) en la base de datos que se va a restaurar.  
  
> [!NOTE]  
>  Después de restaurar una base de datos existente, el usuario que restauró la base de datos podría perder el acceso a la base de datos restaurada. Esta pérdida de acceso puede producirse si, en el momento en que se realizó la copia de seguridad, el usuario no era miembro del rol de servidor o no era miembro de rol de base de datos con permisos de Control total (Administrador).  
  
## <a name="see-also"></a>Vea también  
 [Cuadro de diálogo Restaurar base de datos &#40;Analysis Services - Datos multidimensionales&#41;](../restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Realizar una copia de seguridad y restaurar las bases de datos de Analysis Services](backup-and-restore-of-analysis-services-databases.md)   
 [Elemento Restore &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)   
 [Restaurar, sincronizar y realizar copias de seguridad de bases de datos &#40;XMLA&#41;](../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  

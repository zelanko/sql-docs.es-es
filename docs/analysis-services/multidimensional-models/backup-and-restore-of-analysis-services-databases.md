---
title: "Copia de seguridad y restauración de bases de datos de Analysis Services | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.ssmsimbi.Restore.f1
- sql13.asvs.ssmsimbi.Backup.f1
helpviewer_keywords:
- backing up databases [Analysis Services]
- encryption [Analysis Services]
- databases [Analysis Services], restoring
- cryptography [Analysis Services]
- databases [Analysis Services], backing up
- restoring databases [Analysis Services]
- recovery [Analysis Services]
ms.assetid: 947eebd2-3622-479e-8aa6-57c11836e4ec
caps.latest.revision: 54
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 917761cf40eca3847cd304ec4e2aafb46fc06c5d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="backup-and-restore-of-analysis-services-databases"></a>Realizar una copia de seguridad y restaurar las bases de datos de Analysis Services
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluye copias de seguridad y restauración para poder recuperar una base de datos y sus objetos de un momento determinado. Copias de seguridad y restauración también es una técnica válida para migrar bases de datos a servidores actualizados, mover bases de datos entre servidores o implementar una base de datos en un servidor de producción. Para la recuperación de datos, si aún no tiene un plan de copias de seguridad y los datos son importantes, debe diseñar e implementar un plan lo antes posible.  
  
 Los comandos de copias de seguridad y restauración se realizan en una base de datos de Analysis Services implementada. Para los proyectos y soluciones de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], debe usar el control de código fuente para asegurarse de que puede recuperar las versiones específicas de los archivos de origen y crear un plan de recuperación de datos del repositorio del sistema de control de código fuente utilizado.  
  
 Para realizar una copia de seguridad completa que incluya los datos de origen, debe hacer una copia de seguridad de la base de datos que contiene los datos de detalle. Concretamente, si usa el almacenamiento de base de datos ROLAP o DirectQuery, los datos detallados se almacenan en una base de datos relacional de SQL Server que es distinta de la base de datos de Analysis Services. De lo contrario, si todos los objetos son tabulares o multidimensionales, la copia de seguridad de Analysis Services incluirá los metadatos y los datos de origen.  
  
 Una ventaja evidente de las copias de seguridad automáticas es que la instantánea de los datos siempre estará tan actualizada como determina la frecuencia de la copia de seguridad automática. Las programaciones automatizadas garantizan que no se olvida efectuar copias de seguridad. También puede automatizarse la restauración de una base de datos; ésta puede ser una buena forma de hacer replicaciones de los datos, pero no debe olvidar realizar la copia de seguridad del archivo de clave de cifrado en la instancia donde se hace la replicación. La característica de sincronización se ocupa de la replicación de las bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , pero solo para los datos obsoletos. Todas las características aquí mencionadas pueden implementarse a través de la interfaz de usuario, por medio de comandos XML/A o mediante programación que se ejecuta a través de AMO. Para obtener más información acerca de las estrategias de copia de seguridad, vea el tema acerca de las [estrategias de copia de seguridad con SQL Server 2005 Analysis Services](http://go.microsoft.com/fwlink/?LinkId=81888).  
  
 En este tema se incluyen las secciones siguientes:  
  
-   [Preparación para la copia de seguridad](#bkmk_prep)  
  
-   [Copia de seguridad de una base de datos multidimensional o tabular](#bkmk_cube)  
  
-   [Restaurar una base de datos de Analysis Services](#bkmk_restore)  
  
##  <a name="bkmk_prereq"></a> Requisitos previos  
 Debe tener permisos administrativos en la instancia de Analysis Services o permisos de Control total (administrador) en la base de datos de la que se hace la copia de seguridad.  
  
 La ubicación de restauración debe ser una instancia de Analysis Services que sea de la misma versión o de una versión más reciente, por ejemplo, la instancia a partir de la que se realizó la copia de seguridad. Aunque no puede restaurar una base de datos desde una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a una versión anterior de Analysis Services, una práctica habitual es restaurar una base de datos de la versión anterior, como SQL Server 2012, en una instancia más reciente de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
 La ubicación de restauración debe ser el mismo tipo de servidor. Las bases de datos tabulares se pueden restaurar solo en Analysis Services ejecutándose en modo tabular. Bases de datos multidimensionales requieren una instancia en modo MDX.  
  
##  <a name="bkmk_prep"></a> Preparación para la copia de seguridad  
 Use la siguiente lista de comprobación para preparar la copia de seguridad:  
  
-   Compruebe la ubicación en la que se almacenará el archivo de copia de seguridad. Si usa una ubicación remota, debe especificarla como carpeta UNC. Compruebe que puede tener acceso a la ruta UNC.  
  
-   Compruebe los permisos de la carpeta para asegurarse de que la cuenta de servicio de Analysis Services tenga permisos de lectura/escritura en la carpeta.  
  
-   Compruebe si hay suficiente espacio en disco en el servidor de destino.  
  
-   Compruebe si hay archivos existentes que tengan el mismo nombre. Si ya existe un archivo con el mismo nombre, se producirá un error en la copia de seguridad a menos que especifique opciones para sobrescribir el archivo.  
  
##  <a name="bkmk_cube"></a> Copia de seguridad de una base de datos multidimensional o tabular  
 Los administradores pueden hacer copias de seguridad de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en un único archivo de copia de seguridad de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (.abf), independientemente del tamaño de la base de datos. Para obtener instrucciones paso a paso, vea en TechMantra [How to Backup an Analysis Services Database](http://www.mytechmantra.com/LearnSQLServer/Backup_an_Analysis_Services_Database.html) (Cómo hacer una copia de seguridad de una base de datos de Analysis Services) y [Automate Backup an Analysis Services Database](http://www.mytechmantra.com/LearnSQLServer/Automate_Backup_of_Analysis_Services_Database.html)(Automatizar la copia de seguridad de una base de datos de Analysis Services).  
  
> [!NOTE]  
>  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], utilizado para cargar y consultar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] modelos de datos en un entorno de SharePoint, carga sus modelos desde bases de datos de contenido de SharePoint. Estas bases de datos de contenido son relacionales y se ejecutan en el motor de base de datos relacional de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por tanto, no hay ninguna estrategia de copia de seguridad y restauración de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para los modelos de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Si dispone de un plan de recuperación ante desastres para contenido de SharePoint, ese plan abarca los modelos de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] almacenados en las bases de datos de contenido.  
  
 **Particiones remotas**  
  
 Si la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contiene particiones remotas, estas también deben formar parte de la copia de seguridad. Cuando se hace una copia de seguridad de una base de datos con particiones remotas, se crea una copia de seguridad en un único archivo en cada uno de los servidores remotos de todas las particiones remotas. Por lo tanto, si desea crear esas copias de seguridad fuera de sus respectivos equipos host, deberá copiar manualmente esos archivos en las áreas de almacenamiento designadas.  
  
 **Contenido de un archivo de copia de seguridad**  
  
 La copia de seguridad de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera un archivo de copia de seguridad cuyo contenido varía según el modo de almacenamiento usado por los objetos de la base de datos. Esta diferencia en el contenido de la copia de seguridad se debe al hecho de que cada modo de almacenamiento guarda, en realidad, un conjunto diferente de información de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Por ejemplo, las particiones y dimensiones OLAP híbridas (HOLAP) multidimensionales almacenan agregaciones y metadatos de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , en tanto que las particiones y dimensiones OLAP relacionales (ROLAP) solo almacenan metadatos de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Debido a que el contenido real de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] varía de acuerdo al modo de almacenamiento de cada partición, también varían los contenidos del archivo de copia de seguridad. La siguiente tabla asocia los contenido del archivo de copia de seguridad con el modo de almacenamiento que utilizan los objetos.  
  
|Modo de almacenamiento|Contenidos del archivo de copia de seguridad|  
|------------------|-----------------------------|  
|Particiones y dimensiones MOLAP multidimensionales|Metadatos, datos de origen y agregaciones|  
|Particiones y dimensiones HOLAP multidimensionales|Metadatos y agregaciones|  
|Particiones y dimensiones ROLAP multidimensionales|Metadatos|  
|Modelos tabulares en memoria|Metadatos y datos de origen|  
|Modelos tabulares DirectQuery|Solo metadatos|  
  
> [!NOTE]  
>  Al hacer una copia de seguridad de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no se hace copia de los datos de los orígenes de datos subyacentes, como una base de datos relacional. Solo se hace copia de seguridad del contenido de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Cuando hace una copia de seguridad de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , dispone de las siguientes opciones:  
  
-   Puede comprimir todas las copias de seguridad de la base de datos. La opción predeterminada es comprimir las copias de seguridad.  
  
-   Puede cifrar el contenido de los archivos de copia de seguridad e imponer una contraseña antes de que el archivo pueda descifrarse y restaurarse. De forma predeterminada, los datos de los que se hace copia no se cifran.  
  
    > [!IMPORTANT]  
    >  Para cada archivo de copia de seguridad, el usuario que ejecuta el comando de copia de seguridad debe tener permiso para escribir en la ubicación de copia de seguridad especificada. Además, el usuario debe tener uno de los roles siguientes: miembro de un rol de servidor para la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o miembro de un rol de base de datos con permisos de Control total (Administrador) en la base de datos de la que se va a hacer una copia de seguridad.  
  
 Para obtener más información sobre la copia de seguridad de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , vea [Opciones de copia de seguridad](../../analysis-services/multidimensional-models/backup-options.md).  
  
##  <a name="bkmk_restore"></a> Restaurar una base de datos de Analysis Services  
 Los administradores pueden restaurar una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a partir de uno o más archivos de copia de seguridad.  
  
> [!NOTE]  
>  Si un archivo de copia de seguridad está cifrado, debe proporcionar la contraseña especificada durante la copia de seguridad antes de que pueda usar ese archivo para restaurar una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Durante la restauración, tiene las siguientes opciones:  
  
-   Puede restaurar la base de datos mediante el uso del nombre original de la base de datos o puede especificar un nuevo nombre de base de datos.  
  
-   Puede sobrescribir una base de datos existente. Si elige sobrescribir la base de datos, debe especificar de forma explícita que desea sobrescribirla.  
  
-   Puede elegir si se restaura la información de seguridad existente o se omite la información de seguridad de pertenencia.  
  
-   Puede elegir si el comando de restauración cambia la carpeta de restauración de cada partición que se restaura. Las particiones locales se pueden restaurar en cualquier ubicación de carpeta que sea local para la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] donde se restaura la base de datos. Las particiones remotas se pueden restaurar en cualquier carpeta de cualquier servidor que no sea el servidor local; las particiones remotas no pueden convertirse en locales.  
  
    > [!IMPORTANT]  
    >  Para cada archivo de copia de seguridad, el usuario que ejecuta el comando de restauración debe tener permiso para leer desde la ubicación de la copia de seguridad especificada. Para restaurar una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que no está instalada en el servidor, el usuario también debe ser miembro del rol de servidor para dicha instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para sobrescribir una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , el usuario debe tener uno de los roles siguientes: miembro del rol de servidor para la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o miembro de un rol de base de datos con permisos de Control total (Administrador) en la base de datos que se va a restaurar.  
  
    > [!NOTE]  
    >  Después de restaurar una base de datos existente, el usuario que restauró la base de datos podría perder el acceso a la base de datos restaurada. Esta pérdida de acceso puede producirse si, en el momento en que se realizó la copia de seguridad, el usuario no era miembro del rol de servidor o no era miembro de rol de base de datos con permisos de Control total (Administrador).  
  
 Para obtener más información sobre la restauración de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , vea [Opciones de restauración](../../analysis-services/multidimensional-models/restore-options.md).  
  
## <a name="see-also"></a>Vea también  
 [Restaurar, sincronizar y realizar copias de seguridad de bases de datos &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)   

  
  

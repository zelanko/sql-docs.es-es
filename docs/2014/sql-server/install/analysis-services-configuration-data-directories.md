---
title: Configuración - directorios de datos de Analysis Services | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ef732855-b7af-4f40-a619-5573c1c354bb
caps.latest.revision: 20
author: HeidiSteen
ms.author: heidist
manager: jhubbard
ms.openlocfilehash: b3b945938c0ffd8a5059f8b2c53546538ea97eee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199300"
---
# <a name="analysis-services-configuration---data-directories"></a>Configuración de Analysis Services - Directorios de datos
  Los directorios predeterminados de la tabla siguiente los puede configurar el usuario durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los permisos para obtener acceso a estos archivos se conceden a los administradores locales y a los miembros del grupo de seguridad SQLServerMSASUser$\<instancia> que se crea y aprovisiona durante la instalación.  
  
## <a name="uielement-list"></a>Lista de UIElement  
  
|Descripción|Directorio predeterminado|Recomendaciones|  
|-----------------|-----------------------|---------------------|  
|Directorio raíz de datos|C:\Program Files\Microsoft SQL Server\MSAS12. \<InstanceID > \OLAP\Data\|Asegúrese de que la carpeta de \Program SQL Server\ está protegida con permisos limitados. El rendimiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] depende, en muchas configuraciones, del rendimiento del espacio de almacenamiento en el que se ubica el directorio de datos. Coloque este directorio en el almacenamiento asociado al sistema cuyo rendimiento sea máximo. En las instalaciones del clúster de conmutación por error, asegúrese de que los directorios de datos están ubicados en el disco compartido.|  
|Directorio de archivos de registro|C:\Program Files\Microsoft SQL Server\MSAS12. \<InstanceID > \OLAP\Log\|éste es el directorio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] archivos de registro e incluye el Registro FlightRecorder. Si incrementa la duración de la Caja negra SQL, asegúrese de que el directorio del registro tenga espacio suficiente.|  
|Directorio temporal|C:\Program Files\Microsoft SQL Server\MSAS12. \<InstanceID > \OLAP\Temp\|coloque el directorio Temp en el subsistema de almacenamiento de alto rendimiento.|  
|Directorio de copia de seguridad|C:\Program Files\Microsoft SQL Server\MSAS12. \<InstanceID > \OLAP\Backup\|éste es el directorio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] archivos de copia de seguridad predeterminados. En las instalaciones de PowerPivot para SharePoint, es también donde los Servicios del sistema de PowerPivot almacenan en caché los archivos de datos PowerPivot.<br /><br /> Asegúrese de que se han establecido los permisos adecuados para evitar la pérdida de datos y de que el grupo de usuarios del servicio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tiene los permisos apropiados para escribir en el directorio de copia de seguridad. No se permite usar una unidad asignada para los directorios de copia de seguridad.|  
  
## <a name="notes"></a>Notas  
  
-   Las instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se implementan en una granja de SharePoint almacenan archivos de aplicación, archivos de datos y propiedades de bases de datos de contenido y de aplicación de servicio.  
  
-   Cuando agregue características a una instalación existente, no podrá cambiar la ubicación de una característica instalada anteriormente, ni especificar dicha ubicación para una característica nueva.  
  
-   Si especifica los directorios de instalación no predeterminados, asegúrese de que las carpetas de instalación sean únicas para esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ninguno de los directorios de este cuadro de diálogo se debe compartir con los de otras instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los componentes de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también deben instalarse en directorios independientes.  
  
-   Los archivos de programa y los archivos de datos no se pueden instalar en las situaciones siguientes:  
  
    -   En una unidad de disco extraíble  
  
    -   En un sistema de archivos que usa compresión  
  
    -   En un directorio que contiene archivos del sistema  
  
## <a name="see-also"></a>Vea también  
 [Ubicaciones de archivos para las instancias predeterminadas y con nombre de SQL Server](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)  
  
  
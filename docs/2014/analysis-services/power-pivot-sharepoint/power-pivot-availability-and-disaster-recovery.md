---
title: Disponibilidad de PowerPivot y recuperación ante desastres (SQL Server 2014) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4aaf008c-3bcb-4dbf-862c-65747d1a668c
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 15efd2e1265635fa2870013d580ea4ef929b4600
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37159296"
---
# <a name="powerpivot-availability-and-disaster-recovery-sql-server-2014"></a>Disponibilidad y recuperación ante desastres de PowerPivot (SQL Server 2014)
  Los planes de disponibilidad y de recuperación ante desastres de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] dependen principalmente del diseño de la granja de servidores de SharePoint, el tiempo de inactividad aceptable para los diferentes componentes, y las herramientas y las prácticas recomendadas que se implementan para la disponibilidad de SharePoint. En este tema se resumen las tecnologías y se incluyen diagramas de topología de ejemplo que hay que tener en cuenta al planear la disponibilidad y la recuperación ante desastres para una implementación de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] .  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010|  
  
 **En este tema:**  
  
-   [Ejemplo de topología de SharePoint 2013 de alta disponibilidad de PowerPivot](#bkmk_sharepoint2013)  
  
-   [Ejemplo de topología de SharePoint 2010 para lograr alta disponibilidad de PowerPivot](#bkmk_sharepoint2010)  
  
-   [Tecnologías de disponibilidad y recuperación de la base de datos de aplicación de servicio PowerPivot y SQL Server](#bkmk_sql_server_technologies)  
  
-   [Vínculos a más información](#bkmk_more_resources)  
  
##  <a name="bkmk_sharepoint2013"></a> Ejemplo de topología de SharePoint 2013 de alta disponibilidad de PowerPivot  
 En una implementación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 hay más flexibilidad en cuanto a cómo diseñar la disponibilidad de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . En SharePoint 2013, la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementada en modo de SharePoint, también conocida como servidor de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , se ejecuta fuera de la granja de servidores de SharePoint y se puede instalar en servidores diferentes. Cada instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint se registra con Excel Services. El servicio compartido [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y la aplicación de servicio se ejecuta en servidores de aplicaciones de SharePoint.  
  
 En el diagrama siguiente se muestra una implementación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 de ejemplo. Este ejemplo admite una buena disponibilidad de los servicios de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] y da por supuesto que se hace copia de seguridad de las bases de datos periódicamente.  
  
 ![disponibilidad de PowerPivot en 2013](../media/ssas-powerpivot-services-2013.png "disponibilidad de powerpivot en 2013")  
  
-   **(1)** Los servidores front-end web. Use el complemento [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 para instalar los proveedores de datos en cada servidor. Para obtener más información, consulte [instalar o desinstalar PowerPivot para SharePoint Add-in &#40;SharePoint 2013&#41;](../instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).  
  
-   **(2)** El servicio compartido [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] se ejecuta **en cada** servidor de aplicaciones y permite que la aplicación de servicio se ejecute en **varios servidores de aplicaciones** . Por tanto, si un único servidor de aplicaciones se queda sin conexión, la aplicación [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] sigue estando disponible.  
  
-   **(3)** Excel Calculation Services se ejecuta en cada servidor de aplicaciones y permite que la aplicación de servicio se ejecute en varios servidores de aplicaciones. Por tanto, si un único servidor de aplicaciones se queda sin conexión, Excel Calculation Services sigue estando disponible.  
  
-   **(4)**  y **(6)** instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] inicios de modo de SharePoint se ejecutan en servidores ajenos a la granja de SharePoint; Esto incluye el servicio de Windows **SQL Server Analysis Services (POWERPIVOT)**. Cada una de estas instancias se registra con Excel Services **(3)**. Excel Services administra el equilibrio de carga de las solicitudes a los servidores de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] . La arquitectura de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 permite tener varios servidores para [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] de forma que pueda agregar fácilmente más instancias según sea necesario. Para obtener más información, vea [Administrar la configuración del modelo de datos de Servicios de Excel (SharePoint Server 2013)](http://technet.microsoft.com/library/jj219780\(v=office.15\).aspx).  
  
-   **(5)** Las bases de datos de SQL Server usadas para el contenido, la configuración y las aplicaciones. Esto incluye la base de datos de la aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . El plan de recuperación ante desastres debe incluir la capa de base de datos. En este diseño, las bases de datos se ejecutan en el mismo servidor que **(4)** una de las instancias de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] . **(4)** y **(5)** también pueden estar en servidores diferentes.  
  
-   **(7)** Alguna forma de copia de seguridad o de redundancia de las bases de datos de SQL Server.  
  
##  <a name="bkmk_sharepoint2010"></a> Ejemplo de topología de SharePoint 2010 para lograr alta disponibilidad de PowerPivot  
 La arquitectura de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 requiere que todos los componentes de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] se ejecuten en los mismos servidores de aplicaciones de SharePoint. Esto incluye la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementada en modo de SharePoint y dos servicios compartidos, en lugar de solo uno en el caso de una implementación de SharePoint 2013.  
  
 En el diagrama siguiente se muestra una implementación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 de ejemplo. Este ejemplo admite una buena disponibilidad de los servicios de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] y da por supuesto que se hace copia de seguridad de las bases de datos periódicamente.  
  
 ![disponibilidad de PowerPivot en sharepoint 2010](../media/ssas-powerpivot-services-2010.png "disponibilidad de powerpivot en sharepoint 2010")  
  
-   **(1)** Los servidores front-end web. Instale los proveedores de datos en cada servidor. Para obtener más información, consulte [Instalar el proveedor OLE DB de Analysis Services en servidores de SharePoint](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md).  
  
-   **(2)**  Los dos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] servicios compartidos y **(4)** el servicio de Windows **SQL Server Analysis Services (POWERPIVOT)** están instalados en los servidores de aplicaciones de SharePoint.  
  
     El servicio de sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] se ejecuta **en cada** servidor de aplicaciones y permite que la aplicación de servicio se ejecute en **varios** servidores de aplicaciones. Si un único servidor de aplicaciones se queda sin conexión, la aplicación de servicio [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] sigue estando disponible.  
  
     Para aumentar la capacidad de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en SharePoint 2010, implemente más servidores de aplicaciones de SharePoint que ejecuten el servicio de sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
-   **(3)** Excel Calculation Services se ejecuta en cada servidor de aplicaciones y permite que la aplicación de servicio se ejecute en varios servidores de aplicaciones. Por tanto, si un único servidor de aplicaciones se queda sin conexión, Excel Calculation Services sigue estando disponible.  
  
-   **(5)** Las bases de datos de SQL Server usadas para el contenido, la configuración y las aplicaciones. Esto incluye la base de datos de la aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . El plan de recuperación ante desastres debe incluir la capa de base de datos.  
  
-   **(6)** Alguna forma de copia de seguridad o de redundancia de las bases de datos de SQL Server.  
  
##  <a name="bkmk_sql_server_technologies"></a> Tecnologías de disponibilidad y recuperación de la base de datos de aplicación de servicio PowerPivot y SQL Server  
 Incluya la base de datos de aplicación de servicio de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] en la planeación de alta disponibilidad de SharePoint . El nombre predeterminado de esta base de datos es `DefaultPowerPivotServiceApplicationDB-<GUID>`. El siguiente es un resumen de las tecnologías de disponibilidad y las recomendaciones para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando se usa con la base de datos de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] . Para obtener más información, vea [Compatibilidad de alta disponibilidad y opciones de recuperación ante desastres para bases de datos de SharePoint (SharePoint 2013)](http://technet.microsoft.com/library/jj841106.aspx).  
  
||Comentarios|  
|-|--------------|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] y [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] en una granja de servidores para disponibilidad.|Compatible pero no se recomienda. La recomendación es usar AlwaysOn en modo de confirmación sincrónica.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] en modo de confirmación sincrónica.|Compatible y se recomienda.|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] Creación de reflejo asincrónico o trasvase de registros a otra granja de servidores para la recuperación ante desastres.|Compatible.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] con confirmación asincrónica para recuperación ante desastres.|Admitida|  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Trasvase de registros  
  
 Para obtener más información sobre cómo planear un escenario de espera pasiva con [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], vea [Recuperación ante desastres de PowerPivot](http://social.technet.microsoft.com/wiki/contents/articles/22137.sharepoint-powerpivot-disaster-recovery.aspx).  
  
## <a name="verification"></a>Comprobación  
 Para obtener instrucciones y scripts para ayudarle a comprobar un [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] implementar antes y después de un ciclo de recuperación ante desastres, consulte [lista de comprobación: usar PowerShell para comprobar PowerPivot para SharePoint](../instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint.md).  
  
##  <a name="bkmk_more_resources"></a> Vínculos a más información  
  
-   [Compatibilidad de alta disponibilidad y opciones de recuperación ante desastres para bases de datos de SharePoint (SharePoint 2013)](http://technet.microsoft.com/library/jj841106.aspx)  
  
-   [Planeación de la recuperación ante desastres (SharePoint Server 2010)](http://technet.microsoft.com/library/ff628971\(v=office.14\).aspx)  
  
-   [Notas del producto de copia de seguridad y recuperación en nube de SQL Server](http://www.microsoft.com/server-cloud/solutions/cloud-backup-recovery.aspx?WT.srch=1&WT.mc_ID=SEM_BING_USEvergreenSearch_Unassigned&CR_CC=Unassigned#fbid=RjU2Nbzu2dT)  
  
-   [Herramienta Copia de seguridad de Microsoft® SQL Server Backup en Microsoft Windows® Azure®](http://www.microsoft.com/download/details.aspx?id=40740)  
  
 **Contenido de la comunidad**  
  
-   [Administrar instancias de servicio en SharePoint 2013](http://www.petri.co.il/manage-service-instances-sharepoint-2013.htm)  
  
-   [Script de copia de seguridad de la base de datos SQL Server](http://megaupl0ad.net/free/backup%20database%20sql%20server%20script)  
  
  

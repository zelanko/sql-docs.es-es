---
title: Requisitos de hardware y software para Reporting Services en modo de SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ed91877d-4f74-4266-a932-b824b4810c99
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 56ddfce4fc1812e99870c22eeb0e15be64c5decb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "75245634"
---
# <a name="hardware-and-software-requirements-for-reporting-services-in-sharepoint-mode"></a>Requisitos de hardware y software para Reporting Services en modo de SharePoint

  En este tema se describen los requisitos previos, los requisitos de hardware [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y las consideraciones de instalación para ejecutar en modo de SharePoint. Puesto que el modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] requiere un servidor de SharePoint, la mayoría de los requisitos se basan en el entorno de SharePoint. Para los servidores de informes en modo nativo, el hardware debe cumplir los requisitos mínimos de hardware y software para ejecutar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información, vea [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   [Requisitos previos](#bkmk_prereq)  
  
-   [Requisitos de base de datos del servidor de informes](#bkmk_report_server_database)  
  
-   [Requisitos de la vista avanzada](#bkmk_powerview)  
  
-   [Más información](#bkmk_more_information)  
  
##  <a name="bkmk_prereq"></a> Requisitos previos  
  
-   Para las instalaciones locales, la cuenta con la que se ha iniciado sesión durante la instalación de SharePoint y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] debe ser miembro del grupo de administradores del sistema operativo local. No es necesario que la cuenta de instalación sea miembro del grupo administradores de la granja de SharePoint.  
  
     Para obtener más información, vea [Configurar la seguridad y los permisos de cuenta en SharePoint 2013](https://technet.microsoft.com/library/cc678863.aspx).  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]la ejecución en modo de SharePoint requiere SharePoint Server. Para obtener más información acerca de los requisitos y las configuraciones de SharePoint, vea lo siguiente:  
  
    -   [Requisitos de hardware y software (SharePoint 2013)](https://go.microsoft.com/fwlink/p/?LinkId=256365) (https://go.microsoft.com/fwlink/p/?LinkId=256365)  
  
    -   [Administración y ajuste de tamaño de la capacidad para SharePoint Server 2013](https://technet.microsoft.com/library/cc261700.aspx)  
  
    -   [Requisitos de software para Business Intelligence (SharePoint 2013)](https://go.microsoft.com/fwlink/p/?LinkId=256367)  
  
    -   [Requisitos de hardware y software (SharePoint Server 2010)](https://technet.microsoft.com/library/cc262485\(v=office.14\))  
  
    -   [Administración y ajuste de tamaño de la capacidad de SharePoint Server 2010](https://technet.microsoft.com/library/cc261700.aspx\(v=office.14\))  
  
-   Si desea actualizar una instalación existente de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], vea [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
-   Compruebe que el servicio **Administración de SharePoint 2013** está iniciado en Windows Server Manager.  
  
###  <a name="bkmk_report_server_database"></a>Requisitos de base de datos del servidor de informes  
  
-   Tanto [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] como Productos y tecnologías de SharePoint usan bases de datos relacionales de SQL Server para almacenar datos de aplicaciones.  
  
-   [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]requiere una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] de una edición de SQL Server compatible. Para obtener más información sobre los requisitos de hardware y software, vea [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Los productos de SharePoint pueden utilizar una instancia de base de datos existente. Si no se instala ninguna instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , el programa de instalación de Productos de SharePoint instala SQL Server Express Edition para las bases de datos de aplicación de SharePoint.  
  
-   La instancia del servidor de informes no puede utilizar SQL Server Express Edition para su base de datos. Sin embargo, la instancia de SQL Server Express Edition instalada por el producto de SharePoint puede coexistir con otras ediciones del Motor de base de datos.  
  
##  <a name="bkmk_powerview"></a>[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] Requisitos de

 Examine la [documentación de Power View](https://office.microsoft.com/excel-help/power-view-explore-visualize-and-present-your-data-HA102835634.aspx) más actualizada en Office.Microsoft.com. [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]es una característica de Microsoft Excel 2013 y forma parte del complemento de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Reporting Services para las ediciones Enterprise de Microsoft SharePoint Server 2010 y 2013.  
  
##  <a name="bkmk_more_information"></a> Más información

 Para obtener información sobre los cambios de SharePoint, vea [cambios de sharepoint 2010 a sharepoint 2013](https://technet.microsoft.com/library/ff607742\(office.15\).aspx) (https://technet.microsoft.com/library/ff607742(office.15).aspx).  
  
 [SQL Server notas](https://go.microsoft.com/fwlink/?LinkID=296445)de la versión de 2014.  
  

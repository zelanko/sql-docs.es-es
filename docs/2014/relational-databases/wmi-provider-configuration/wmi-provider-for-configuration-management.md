---
title: Proveedor WMI para conocer los conceptos de administración de configuración | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management
- SQL Server WMI Provider
- configuration management [WMI]
- WMI Provider for Configuration Management, about WMI Provider for Configuration Management
ms.assetid: 7e41db24-b915-4eb8-a1d6-e6948ee915b7
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: dfa4b21eb44e3462d9f8d95bed2f09b5c4747d22
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48095065"
---
# <a name="wmi-provider-for-configuration-management-concepts"></a>Conceptos del proveedor WMI de administración de configuración
  El proveedor WMI es un nivel publicado que se usa con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el complemento Administrador de configuración de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (MMC) y la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. Proporciona una forma unificada de crear una interfaz con las llamadas a la API que administran las operaciones del Registro solicitadas por el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y proporciona un mejor control y manipulación de los servicios SQL seleccionados del complemento Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 El proveedor WMI de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es una DLL y un archivo MOF que compila automáticamente el Programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 El proveedor WMI de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene un conjunto de clases de objeto que se utiliza para controlar los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando los métodos siguientes:  
  
-   Un lenguaje de script como VBScript, [!INCLUDE[jsprjscript](../../includes/jsprjscript-md.md)] o Perl, en los que se puede incrustar el Lenguaje de consulta de Windows (WQL).  
  
-   El objeto <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> en un programa de código administrado de SMO.  
  
-   El Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o MMC con el complemento del proveedor WMI de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="using-a-script-language"></a>Utilizar un lenguaje de script  
 Las ventajas de usar un lenguaje de script son las siguientes:  
  
-   No se requiere un entorno de desarrollo.  
  
-   Los archivos que admiten el lenguaje de script están ampliamente disponibles.  
  
 El script también puede funcionar con otros proveedores WMI además del proveedor WMI de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un administrador de dominio puede utilizar un script para configurar los servicios, la configuración de la red y los valores de alias en varios equipos de una red.  
  
 En esta sección se explica con más detalle cómo tener acceso al proveedor WMI de Administración de configuración a partir de scripts.  
  
## <a name="using-the-smo-managedcomputer-object"></a>Utilizar el objeto ManagedComputer de SMO  
 El objeto <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> es un objeto SMO administrado que proporciona acceso al proveedor WMI para la Administración de configuración. Si se utiliza un programa SMO, se puede usar el objeto <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> para ver y modificar servicios, la configuración de red y valores de alias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [administrar servicios y la configuración de red utilizando el proveedor de WMI](../server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md).  
  
## <a name="using-the-microsoft-management-console-or-sql-server-configuration-manager"></a>Utilizar Microsoft Management Console o el Administrador de configuración de SQL Server  
 Microsoft Management Console (MMC) proporciona una interfaz para administrar los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a diferencia de un lenguaje de scripting o un programa de código administrado. El complemento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Console se puede utilizar para detener e iniciar servicios y para cambiar las cuentas de servicio.  
  
 El Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se puede utilizar también para administrar servicios, protocolos de servidor, protocolos de cliente y servidor y alias de cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Descripción del proveedor WMI para la administración de configuración](understanding-the-wmi-provider-for-configuration-management.md)   
 [Trabajar con el proveedor WMI para la administración de configuración](working-with-the-wmi-provider-for-configuration-management.md)   
 [Uso de WQL y lenguajes de scripting con el proveedor WMI para la administración de configuración](using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  

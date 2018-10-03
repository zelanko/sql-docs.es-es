---
title: Uso de WQL y lenguajes de Scripting con el proveedor WMI de administración de configuración | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- queries [WMI]
- scripts [WMI]
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
- WMI Provider for Configuration Management, scripts
ms.assetid: c1e64905-3c2b-4974-88f4-abf17cf7e289
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: be5442f46db4d0c51b876d50d99b9feb7a25e239
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48157813"
---
# <a name="using-wql-and-scripting-languages-with-the-wmi-provider-for-configuration-management"></a>Utilizar WQL y languages de scripting con el proveedor WMI para la administración de configuración
  Las aplicaciones de administración obtienen acceso a los servicios y la configuración de red de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante el proveedor de Instrumental de administración de Windows (WMI) para los objetos de administración de configuración de dos maneras:  
  
-   Mediante un editor WQL o herramienta de consulta, como WBEMTest.exe, para consultar el objeto establecido con el lenguaje (WQL) del Instrumental de administración de Windows.  
  
-   Mediante un lenguaje de scripting, como VBScript.  
  
 Alternativamente, los servicios y la configuración de red de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se pueden administrar mediante programación usando los objetos administrados WMI en SMO. Para obtener más información sobre la programación de WMI objetos administrados, consulte [administrar servicios y la configuración de red utilizando el proveedor de WMI](../server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md).  
  
 Se puede tener acceso al proveedor WMI para administración de configuración mediante elAdministrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console. Para obtener más información sobre el acceso al proveedor WMI de una interfaz de usuario, consulte [temas de procedimientos de servicios de administración de &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/managing-services-how-to-topics-sql-server-configuration-manager.md).  
  
## <a name="see-also"></a>Vea también  
 [Acceso al proveedor de WMI para la administración de configuración mediante WQL](access-wmi-provider-for-configuration-management-using-wql.md)   
 [Modificar propiedades avanzadas de servicios SQL Server mediante VBScript](access-wmi-provider-for-configuration-management-using-vbscript.md)  
  
  

---
title: Utilizar WQL y Languages de Scripting con el proveedor WMI | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 18
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ed3b0c63486e00ab4af97895193de8110befd3a8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="using-wql-and-scripting-languages-with-the-wmi-provider"></a>Utilizar WQL y Languages de Scripting con el proveedor WMI
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Las aplicaciones de administración obtienen acceso a los servicios y la configuración de red de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante el proveedor de Instrumental de administración de Windows (WMI) para los objetos de administración de configuración de dos maneras:  
  
-   Mediante un editor WQL o herramienta de consulta, como WBEMTest.exe, para consultar el objeto establecido con el lenguaje (WQL) del Instrumental de administración de Windows.  
  
-   Mediante un lenguaje de scripting, como VBScript.  
  
 Alternativamente, los servicios y la configuración de red de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se pueden administrar mediante programación usando los objetos administrados WMI en SMO. Para obtener más información sobre la programación de WMI objetos administrados, vea [administrar servicios y la configuración de red usando el proveedor de WMI](../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md).  
  
 Se puede tener acceso al proveedor WMI para administración de configuración mediante elAdministrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console. Para obtener más información sobre cómo tener acceso al proveedor WMI de una interfaz de usuario, consulte [temas de procedimientos de servicios de administración de &#40;Administrador de configuración de SQL Server&#41;](http://msdn.microsoft.com/library/78dee169-df0c-4c95-9af7-bf033bc9fdc6).  
  
## <a name="see-also"></a>Vea también  
 [Acceso al proveedor WMI para la administración de configuración mediante WQL](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-wql.md)   
 [Modificar servicio propiedades avanzadas SQL Server mediante VBScript](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-vbscript.md)  
  
  

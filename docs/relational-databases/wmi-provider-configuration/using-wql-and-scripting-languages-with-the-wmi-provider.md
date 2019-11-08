---
title: Acceso al proveedor WMI con WQL y scripting
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
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
ms.openlocfilehash: 66a0af86e5a9939e9f4621b506991f8234d887dd
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2019
ms.locfileid: "73660598"
---
# <a name="using-wql-and-scripting-languages-with-the-wmi-provider"></a>Uso de WQL y lenguajes de scripting con el proveedor WMI
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Las aplicaciones de administración obtienen acceso a los servicios y la configuración de red de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante el proveedor de Instrumental de administración de Windows (WMI) para los objetos de administración de configuración de dos maneras:  
  
-   Mediante un editor WQL o herramienta de consulta, como WBEMTest.exe, para consultar el objeto establecido con el lenguaje (WQL) del Instrumental de administración de Windows.  
  
-   Mediante un lenguaje de scripting, como VBScript.  
  
 Alternativamente, los servicios y la configuración de red de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se pueden administrar mediante programación usando los objetos administrados WMI en SMO. Para obtener más información acerca de la programación de objetos administrados por WMI, vea [administrar servicios y configuración de red mediante el proveedor WMI](../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md).  
  
 Se puede tener acceso al proveedor WMI para administración de configuración mediante elAdministrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console. Para obtener más información sobre el acceso al proveedor WMI desde una interfaz de usuario, consulte los [temas &#40;de procedimientos de&#41;administración de servicios Administrador de configuración de SQL Server](https://msdn.microsoft.com/library/78dee169-df0c-4c95-9af7-bf033bc9fdc6).  
  
## <a name="see-also"></a>Vea también  
 [Obtener acceso al proveedor WMI para la administración de configuración mediante WQL](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-wql.md)   
 [Obtener acceso al proveedor WMI con VBScript](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-vbscript.md)  
  
  

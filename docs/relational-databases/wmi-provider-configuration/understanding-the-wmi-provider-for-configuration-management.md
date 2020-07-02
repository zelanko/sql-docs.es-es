---
title: proveedor WMI de administración de configuración
description: Obtenga información acerca de cómo el proveedor WMI para la administración de configuración usa WMI para administrar los servicios, los alias de servidor y la configuración de red de cliente/servidor en SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management, operations supported
ms.assetid: 92323972-7943-4208-bbf4-050774fb6027
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d517a674840f9115a80600838f5c401c5d586a9a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729987"
---
# <a name="understanding-the-wmi-provider-for-configuration-management"></a>Descripción del proveedor WMI para la administración de configuración
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]proporciona el proveedor WMI para la administración de la configuración. Esto permite usar Instrumental de administración de Windows (WMI) para administrar servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], configuración de red de cliente y servidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y alias de servidor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]los objetos WMI representan los servicios, la configuración de red y los alias en el espacio de nombres root\Microsoft\SqlServer\ComputerManagement*nn* del equipo. Una vez establecida una conexión con el proveedor WMI en el equipo especificado, se pueden consultar los servicios, la configuración de red y el alias mediante WQL o un lenguaje de scripting.  
  
 El Proveedor WMI es un proveedor de instancias. Proporciona instancias de las [clases de WMI](../../relational-databases/wmi-provider-configuration-classes/wmi-provider-for-configuration-management-classes.md) y admite las siguientes operaciones asincrónicas.  
  
 Recuperación de instancias  
 Recuperación de una instancia de tipo de clase determinada.  
  
 Enumeración  
 Enumeración de todas las instancias de un tipo de clase.  
  
 Modificación  
 Modificación de una instancia de tipo de clase determinada.  
  
 Las clases tienen métodos que permiten modificar sus propiedades.  
  
 Eliminación  
 Quita una instancia de tipo de clase determinada.  
  
 Procesamiento de consultas  
 La enumeración de instancias de un tipo de clase basada en un filtro.  
  
 Para ver ejemplos de aplicaciones de administración que usan el proveedor WMI para la administración de configuración, consulte [uso de WQL y lenguajes de scripting con el proveedor WMI para la administración de la configuración](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md).  
  
 Para obtener más información acerca de la programación de aplicaciones de administración mediante el proveedor WMI, vea la documentación de WMI en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] SDK de .NET Framework.  
  
## <a name="see-also"></a>Consulte también  
 [Trabajar con el proveedor WMI para la administración de configuración](../../relational-databases/wmi-provider-configuration/working-with-the-wmi-provider-for-configuration-management.md)   
 [Utilizar WQL y languages de scripting con el proveedor WMI para la administración de configuración](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  

---
title: Descripción del proveedor WMI para la administración de configuración | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management, operations supported
ms.assetid: 92323972-7943-4208-bbf4-050774fb6027
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 459bb3bb7843a0f962d9747ac702da23909ca9fc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201998"
---
# <a name="understanding-the-wmi-provider-for-configuration-management"></a>Descripción del proveedor WMI para la administración de configuración
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona el proveedor WMI para la administración de configuración. Esto permite usar Instrumental de administración de Windows (WMI) para administrar servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], configuración de red de cliente y servidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y alias de servidor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicios, configuración de red y alias se representan mediante objetos WMI en el root\Microsoft\SqlServer\ComputerManagement*nn* espacio de nombres del equipo. Una vez establecida una conexión con el proveedor WMI en el equipo especificado, se pueden consultar los servicios, la configuración de red y el alias mediante WQL o un lenguaje de scripting.  
  
 El Proveedor WMI es un proveedor de instancias. Proporciona instancias de la [clases WMI](../wmi-provider-configuration-classes/wmi-provider-for-configuration-management-classes.md) y es compatible con las operaciones asincrónicas siguientes.  
  
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
  
 Para obtener ejemplos de aplicación de administración mediante el proveedor de WMI para la administración de configuración, consulte [usar WQL y lenguajes de secuencias de comandos con el proveedor de WMI para la administración de configuración](using-wql-and-scripting-languages-with-the-wmi-provider.md).  
  
 Para obtener más información sobre la programación de aplicaciones de administración mediante el proveedor de WMI, vea la documentación de WMI en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework SDK.  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con el proveedor WMI para la administración de configuración](working-with-the-wmi-provider-for-configuration-management.md)   
 [Utilizar WQL y Languages de Scripting con el proveedor WMI para la administración de configuración](using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
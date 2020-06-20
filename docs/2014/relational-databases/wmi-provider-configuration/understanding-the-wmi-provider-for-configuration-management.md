---
title: Descripción del proveedor WMI para la administración de configuración | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management, operations supported
ms.assetid: 92323972-7943-4208-bbf4-050774fb6027
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a2ecd601b1329b3b95f1c3827cd04775c93304f6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061278"
---
# <a name="understanding-the-wmi-provider-for-configuration-management"></a>Descripción del proveedor WMI para la administración de configuración
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]proporciona el proveedor WMI para la administración de la configuración. Esto permite usar Instrumental de administración de Windows (WMI) para administrar servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], configuración de red de cliente y servidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y alias de servidor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]los objetos WMI representan los servicios, la configuración de red y los alias en el espacio de nombres root\Microsoft\SqlServer\ComputerManagement*nn* del equipo. Una vez establecida una conexión con el proveedor WMI en el equipo especificado, se pueden consultar los servicios, la configuración de red y el alias mediante WQL o un lenguaje de scripting.  
  
 El Proveedor WMI es un proveedor de instancias. Proporciona instancias de las [clases de WMI](../wmi-provider-configuration-classes/wmi-provider-for-configuration-management-classes.md) y admite las siguientes operaciones asincrónicas.  
  
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
  
 Para ver ejemplos de aplicaciones de administración que usan el proveedor WMI para la administración de configuración, consulte [uso de WQL y lenguajes de scripting con el proveedor WMI para la administración de la configuración](using-wql-and-scripting-languages-with-the-wmi-provider.md).  
  
 Para obtener más información acerca de la programación de aplicaciones de administración mediante el proveedor WMI, vea la documentación de WMI en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] SDK de .NET Framework.  
  
## <a name="see-also"></a>Consulte también  
 [Trabajar con el proveedor WMI para la administración de configuración](working-with-the-wmi-provider-for-configuration-management.md)   
 [Utilizar WQL y languages de scripting con el proveedor WMI para la administración de configuración](using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  

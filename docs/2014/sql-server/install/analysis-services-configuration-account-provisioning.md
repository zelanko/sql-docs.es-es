---
title: Analysis Services - configuración de aprovisionamiento de cuentas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services configuration
- account provisioning
ms.assetid: 169b1af2-6fe2-467f-8ca4-919f24c620ce
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: 033c1ec1b0ad478e525f3ea9e8f172c5e5e31eef
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66096795"
---
# <a name="analysis-services-configuration---account-provisioning"></a>Configuración de Analysis Services - Aprovisionamiento de cuentas
  Use esta página para establecer el modo de servidor y para conceder permisos administrativos a los usuarios o servicios que requieran acceso sin restricciones a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La instalación no agrega automáticamente el grupo Windows local BUILTIN\Administrators al rol de administrador del servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de la instancia que está instalando. Si desea agregar el grupo local de administradores al rol de administrador del servidor, debe especificar ese grupo explícitamente.  
  
 Si está instalando [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], asegúrese de conceder permisos administrativos a los administradores de la granja de SharePoint o a los administradores de servicios que sean responsables de una implementación del servidor de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en una granja de [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]. Para obtener más información acerca de [!INCLUDE[ssGeminiMTS](../../includes/ssgeminimts-md.md)] instalación y los requisitos de la cuenta de servicio, vea [instalar características de BI de SQL Server con SharePoint &#40;PowerPivot y Reporting Services&#41;](../../../2014/sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md).  
  
## <a name="options"></a>Opciones  
 **Modo de servidor** : permite especificar el tipo de bases de datos de Analysis Services que se pueden implementar en el servidor. Los modos de servidor se determinan durante la instalación y no se pueden modificar posteriormente. Cada modo es mutuamente exclusivo, lo que significa que se necesitarán dos instancias de Analysis Services, cada una configurada para un modo diferente, para admitir soluciones de modelo OLAP clásicas y tabulares.  
  
 **Especificar administradores** Debe especificar al menos un administrador de servidor para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los usuarios o grupos que especifique serán miembros del rol de administrador del servidor de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que está instalando. Debe haber cuentas de usuario de dominio de Windows en el mismo dominio que el del equipo en el que se instala el software.  
  
> [!NOTE]  
>  Control de cuentas de usuario (UAC) es una característica de seguridad de Windows que requiere que un administrador apruebe específicamente acciones administrativas o aplicaciones antes de que se puedan ejecutar. Dado que UAC está activado de forma predeterminada, se le solicitará que permita las operaciones concretas que requieren privilegios elevados. Puede configurar UAC para cambiar el comportamiento predeterminado o personalizar UAC para programas concretos. Para más información sobre UAC y la configuración de UAC, consulte [Guía paso a paso de Control de cuentas de usuario](https://go.microsoft.com/fwlink/?linkid=196350) y el tema sobre [control de cuentas de usuario (Wikipedia)](https://go.microsoft.com/fwlink/?linkid=196351).  
  
## <a name="see-also"></a>Vea también  
 [Configurar cuentas de servicio &#40;Analysis Services&#41;](../../../2014/analysis-services/instances/configure-service-accounts-analysis-services.md)   
 [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  

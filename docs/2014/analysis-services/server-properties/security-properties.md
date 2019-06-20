---
title: Propiedades de seguridad | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- security [Analysis Services], properties
- SecurityPackageList property
- BuiltinAdminsAreServerAdmins property
- DisableClientImpersonation property
- ErrorMessageMode property
- RequiredProtectionLevel property
- ServiceAccountIsServerAdmin property
- RequireClientAuthentication property
ms.assetid: 2fc7fe10-0cbb-49ac-aa8c-8ec3f7a7705f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9316827245adfbcf64bd798869f570dc5f0af14c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068907"
---
# <a name="security-properties"></a>Propiedades de seguridad
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite las propiedades de servidor de seguridad que aparecen en la tabla siguiente. Para obtener más información sobre las propiedades de servidor adicionales y cómo establecerlas, vea [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md).  
  
 **Se aplica a:** Modo de servidor multidimensional y Tabular  
  
## <a name="properties"></a>Propiedades  
 `RequireClientAuthentication`  
 Propiedad booleana que indica si se necesita la autenticación del cliente.  
  
 El valor predeterminado de esta propiedad es True, lo que indica que se necesita la autenticación del cliente.  
  
 `SecurityPackageList`  
 Propiedad de cadena que contiene una lista separada por comas de los paquetes SSPI utilizados por el servidor para la autenticación del cliente.  
  
 `DisableClientImpersonation`  
 Propiedad booleana que indica si la suplantación del cliente (por ejemplo desde los procedimientos almacenados) está deshabilitada.  
  
 El valor predeterminado de esta propiedad es False, lo que indica que la suplantación del cliente está habilitada.  
  
 `BuiltinAdminsAreServerAdmins`  
 Propiedad booleana que indica si los miembros del grupo de administradores del equipo local son administradores de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 `ServiceAccountIsServerAdmin`  
 Propiedad booleana que indica si la cuenta de servicio es un administrador de servidor.  
  
 El valor predeterminado de esta propiedad es True, lo que indica que la cuenta de servicio es un administrador de servidor.  
  
 `ErrorMessageMode`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `DataProtection\ RequiredProtectionLevel`  
 Propiedad de entero de 32 bits con firma que define el nivel de protección necesario para todas las solicitudes de cliente. Esta propiedad tiene uno de los valores indicados en la siguiente tabla.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*0*|Ninguno, se permite texto no cifrado.|  
|*1*|(Valor predeterminado) Se exige cifrado, no se permite iniciar sesión con texto no cifrado.|  
|*2*|Se permiten las solicitudes con texto no cifrado, pero solo con firma (protección más débil que el cifrado).|  
  
 `AdministrativeDataProtection\ RequiredProtectionLevel`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Configurar las propiedades del servidor en Analysis Services](server-properties-in-analysis-services.md)   
 [Determinar el modo de servidor de una instancia de Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  

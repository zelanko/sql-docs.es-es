---
title: Propiedades de seguridad | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
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
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f1857b8cba9f789a7f3ef470dee0e1f728e4ae3d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="security-properties"></a>Propiedades de seguridad
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite las propiedades de servidor de seguridad que aparecen en la tabla siguiente. Para obtener más información sobre otras propiedades de servidor y cómo establecerlas, vea [Configurar las propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Se aplica a:** modo de servidor multidimensional y tabular  
  
## <a name="properties"></a>Propiedades  
 **RequireClientAuthentication**  
 Propiedad booleana que indica si se necesita la autenticación del cliente.  
  
 El valor predeterminado de esta propiedad es True, lo que indica que se necesita la autenticación del cliente.  
  
 **SecurityPackageList**  
 Propiedad de cadena que contiene una lista separada por comas de los paquetes SSPI utilizados por el servidor para la autenticación del cliente.  
  
 **DisableClientImpersonation**  
 Propiedad booleana que indica si la suplantación del cliente (por ejemplo desde los procedimientos almacenados) está deshabilitada.  
  
 El valor predeterminado de esta propiedad es False, lo que indica que la suplantación del cliente está habilitada.  
  
 **BuiltinAdminsAreServerAdmins**  
 Propiedad booleana que indica si los miembros del grupo de administradores del equipo local son administradores de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 **ServiceAccountIsServerAdmin**  
 Propiedad booleana que indica si la cuenta de servicio es un administrador de servidor.  
  
 El valor predeterminado de esta propiedad es True, lo que indica que la cuenta de servicio es un administrador de servidor.  
  
 **ErrorMessageMode**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataProtection\ RequiredProtectionLevel**  
 Propiedad de entero de 32 bits con firma que define el nivel de protección necesario para todas las solicitudes de cliente. Esta propiedad tiene uno de los valores indicados en la siguiente tabla.  
  
|Value|Descripción|  
|-----------|-----------------|  
|*0*|Ninguno, se permite texto no cifrado.|  
|*1*|(Valor predeterminado) Se exige cifrado, no se permite iniciar sesión con texto no cifrado.|  
|*2*|Se permiten las solicitudes con texto no cifrado, pero solo con firma (protección más débil que el cifrado).|  
  
 **AdministrativeDataProtection\ RequiredProtectionLevel**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determinar el modo de servidor de una instancia de Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  

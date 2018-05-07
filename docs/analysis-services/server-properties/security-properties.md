---
title: Propiedades de seguridad | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8c587bbe18f99779889960a94f68ad43bde59b76
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
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
  
  

---
title: Programación de la integración de CLR y de atributos de protección de host | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- HostProtectionAttribute [CLR integration]
- common language runtime [SQL Server], host protection attributes
- disallowed types and members [CLR integration]
- common language runtime [SQL Server], disallowed types and members
- HPAs [CLR integration]
ms.assetid: 268078df-63ca-4c03-a8e7-7108bcea9697
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 68f1f114002ab0ef38c7565a523723a06958048d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205595"
---
# <a name="host-protection-attributes-and-clr-integration-programming"></a>Atributos de protección del host y programación de la integración CLR
  El Common Language Runtime (CLR) proporciona un mecanismo para anotar interfaces de programación de aplicaciones (API) administradas que forman parte del .NET Framework con ciertos atributos que pueden ser de interés para un host del CLR, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que se inició con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Los ejemplos de estos atributos de protección del host (HPA) incluyen:  
  
-   `SharedState`, que indica si la API expone la capacidad para crear o administrar el estado compartido (por ejemplo, campos clase estática).  
  
-   `Synchronization`, que indica si la API expone la capacidad de realizar la sincronización entre los subprocesos.  
  
-   `ExternalProcessMgmt`, que indica si la API expone una manera de controlar el proceso de host.  
  
 Al proporcionar estos atributos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especifica una lista de los HPA que no se permiten en el entorno hospedado a través de la seguridad de acceso del código (CAS). Los requisitos de CAS se especifican mediante uno de los tres conjuntos de permisos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: `SAFE`, `EXTERNAL_ACCESS` o `UNSAFE`. Uno de estos tres niveles de seguridad se especifica cuando el ensamblado se registra en el servidor mediante la instrucción `CREATE ASSEMBLY`. La ejecución de códigos desde los conjuntos de permiso `SAFE` o `EXTERNAL_ACCESS` debe evitar ciertos tipos o miembros que tienen aplicado el atributo `System.Security.Permissions.HostProtectionAttribute`. Para obtener más información, consulte [creación de un ensamblado](../clr-integration/assemblies/creating-an-assembly.md) y [restricciones del modelo de programación de integración de CLR](../clr-integration/database-objects/clr-integration-programming-model-restrictions.md).  
  
 El atributo `HostProtectionAttribute` no es tanto un permiso de seguridad como una manera de mejorar la confiabilidad, en cuanto a que identifica construcciones de código específicas, bien sean tipos o métodos, que pueden no estar permitidas por el host. El uso del atributo `HostProtectionAttribute` exige un modelo de programación de ayuda para proteger la estabilidad del host.  
  
## <a name="host-protection-attributes"></a>Atributos de protección del host  
 Los HPA identifican los tipos o miembros que no se ajustan al modelo de programación del host y representan los siguientes niveles crecientes de amenaza de confiabilidad:  
  
-   En caso contrario son favorables.  
  
-   Podrían provocar la desestabilización del código de usuario administrado por servidor.  
  
-   Podría provocar la desestabilización del propio proceso de servidor.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite el uso de un tipo o miembro que tiene un `HostProtectionAttribute` que especifica un `System.Security.Permissions.HostProtectionResource` enumeración con un valor de `ExternalProcessMgmt`, `ExternalThreading`, `MayLeakOnAbort`, `SecurityInfrastructure`, `SelfAffectingProcessMgmnt`, `SelfAffectingThreading`, `SharedState`, `Synchronization`, o `UI`. De esta forma, se evita que los ensamblados llamen a miembros que habiliten el estado compartido, ejecuten la sincronización, puedan causar una pérdida de recursos al terminar o afecten la integridad de los procesos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="disallowed-types-and-members"></a>Tipos y miembros no permitidos  
 En los temas siguientes se identifican los tipos y miembros cuyos valores `HostProtectionResource` no se permiten en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Las listas de estos temas se generaron a partir de los ensamblados admitidos.  Para obtener más información, consulte [admite bibliotecas de .NET Framework](../clr-integration/database-objects/supported-net-framework-libraries.md).  
  
## <a name="in-this-section"></a>En esta sección  
 [Miembros y tipos no permitidos en Microsoft.VisualBasic.dll](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)  
 Enumera los tipos y miembros de Microsoft.VisualBasic.dll cuyos valores de HPA no se permiten.  
  
 [Miembros y tipos no permitidos en mscorlib.dll](disallowed-types-and-members-in-mscorlib-dll.md)  
 Enumera los tipos y miembros en mscorlib.dll cuyos valores HPA no se permiten.  
  
 [Tipos y miembros no permitidos en System.dll](disallowed-types-and-members-in-system-dll.md)  
 Enumera los tipos y miembros en System.dll cuyos valores HPA no se permiten.  
  
 [Tipos y miembros no permitidos en System.Data.dll](disallowed-types-and-members-in-system-data-dll.md)  
 Enumera los tipos y miembros en System.Data.dll cuyos valores HPA no se permiten.  
  
 [Tipos y miembros no permitidos en System.Core.dll](disallowed-types-and-members-in-system-core-dll.md)  
 Enumera los tipos y miembros en System.Core.dll cuyos valores HPA no se permiten.  
  
## <a name="see-also"></a>Vea también  
 [Seguridad de acceso del código de integración de CLR](../clr-integration/security/clr-integration-code-access-security.md)   
 [Restricciones del modelo de programación de integración de CLR](../clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Crear un ensamblado](../clr-integration/assemblies/creating-an-assembly.md)  
  
  

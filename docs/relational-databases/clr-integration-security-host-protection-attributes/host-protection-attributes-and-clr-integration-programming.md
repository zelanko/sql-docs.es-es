---
title: Atributos de protección del host de Common Language Runtime (CLR)
description: CLR proporciona un mecanismo para anotar las API administradas en el .NET Framework con atributos como SharedState, Synchronization y ExternalProcessMgmt.
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
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
ms.openlocfilehash: 2aeaeb5d4eb06d6d632a59300225d01cc4376369
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488064"
---
# <a name="host-protection-attributes-and-clr-integration-programming"></a>Atributos de protección del host y programación de la integración CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El Common Language Runtime (CLR) proporciona un mecanismo para anotar interfaces de programación de aplicaciones (API) administradas que forman parte del .NET Framework con ciertos atributos que pueden ser de interés para un host del CLR, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que se inició con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Los ejemplos de estos atributos de protección del host (HPA) incluyen:  
  
-   **SharedState**, que indica si la API expone la capacidad de crear o administrar el estado compartido (por ejemplo, campos de clase estáticos).  
  
-   **Sincronización**, que indica si la API expone la capacidad de realizar la sincronización entre subprocesos.  
  
-   **ExternalProcessMgmt**, que indica si la API expone una manera de controlar el proceso de host.  
  
 Al proporcionar estos atributos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especifica una lista de los HPA que no se permiten en el entorno hospedado a través de la seguridad de acceso del código (CAS). Los requisitos de CAS se especifican mediante uno [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de los tres conjuntos de permisos: **Safe**, **external_access**o **Unsafe**. Uno de estos tres niveles de seguridad se especifica cuando el ensamblado se registra en el servidor mediante la instrucción **Create Assembly** . El código que se ejecuta dentro de los conjuntos de permisos **Safe** o **external_access** debe evitar ciertos tipos o miembros que tienen aplicado el atributo **System. Security. Permissions. HostProtectionAttribute** . Para obtener más información, vea [crear un ensamblado](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md) y restricciones del modelo de programación de la [integración CLR](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md).  
  
 **HostProtectionAttribute** no es un permiso de seguridad, ya que se trata de una manera de mejorar la confiabilidad, ya que identifica construcciones de código específicas, ya sean tipos o métodos, que el host puede impedir. El uso de **HostProtectionAttribute** aplica un modelo de programación que ayuda a proteger la estabilidad del host.  
  
## <a name="host-protection-attributes"></a>Atributos de protección del host  
 Los HPA identifican los tipos o miembros que no se ajustan al modelo de programación del host y representan los siguientes niveles crecientes de amenaza de confiabilidad:  
  
-   En caso contrario son favorables.  
  
-   Podrían provocar la desestabilización del código de usuario administrado por servidor.  
  
-   Podría provocar la desestabilización del propio proceso de servidor.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]no permite el uso de un tipo o miembro que tiene un **HostProtectionAttribute** que especifica una enumeración **System. Security. Permissions. HostProtectionResource** con un valor de **ExternalProcessMgmt**, **ExternalThreading**, **MayLeakOnAbort**, **SecurityInfrastructure**, **SelfAffectingProcessMgmnt**, **SelfAffectingThreading**, **SharedState**, **Synchronization**o **UI**. De esta forma, se evita que los ensamblados llamen a miembros que habiliten el estado compartido, ejecuten la sincronización, puedan causar una pérdida de recursos al terminar o afecten la integridad de los procesos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="disallowed-types-and-members"></a>Tipos y miembros no permitidos  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]los temas siguientes se identifican los tipos y miembros cuyos valores de **HostProtectionResource** no se permiten.  
  
> [!NOTE]  
>  Las listas de estos temas se generaron a partir de los ensamblados admitidos.  Para obtener más información, consulte [supported .NET Framework Libraries](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
## <a name="in-this-section"></a>En esta sección  
 [Miembros y tipos no permitidos en Microsoft.VisualBasic.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)  
 Enumera los tipos y miembros de Microsoft.VisualBasic.dll cuyos valores de HPA no se permiten.  
  
 [Miembros y tipos no permitidos en mscorlib.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)  
 Enumera los tipos y miembros en mscorlib.dll cuyos valores HPA no se permiten.  
  
 [Tipos y miembros no permitidos en System.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)  
 Enumera los tipos y miembros en System.dll cuyos valores HPA no se permiten.  
  
 [Tipos y miembros no permitidos en System.Data.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-data-dll.md)  
 Enumera los tipos y miembros en System.Data.dll cuyos valores HPA no se permiten.  
  
 [Tipos y miembros no permitidos en System.Core.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
 Enumera los tipos y miembros en System.Core.dll cuyos valores HPA no se permiten.  
  
## <a name="see-also"></a>Consulte también  
 [Seguridad de acceso del código de integración CLR](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Restricciones del modelo de programación de la integración CLR](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Crear un ensamblado](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  

---
title: Atributos de protección y la programación de la integración de CLR de host | Documentos de Microsoft
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- HostProtectionAttribute [CLR integration]
- common language runtime [SQL Server], host protection attributes
- disallowed types and members [CLR integration]
- common language runtime [SQL Server], disallowed types and members
- HPAs [CLR integration]
ms.assetid: 268078df-63ca-4c03-a8e7-7108bcea9697
caps.latest.revision: 28
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bd3b430f3556eba9d6f9b510aa813bec2a6c9ad3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="host-protection-attributes-and-clr-integration-programming"></a>Atributos de protección del host y programación de la integración CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El Common Language Runtime (CLR) proporciona un mecanismo para anotar interfaces de programación de aplicaciones (API) administradas que forman parte del .NET Framework con ciertos atributos que pueden ser de interés para un host del CLR, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que se inició con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Los ejemplos de estos atributos de protección del host (HPA) incluyen:  
  
-   **SharedState**, lo que indica si la API expone la capacidad de crear o administrar el estado (por ejemplo, los campos de clase estática) compartido.  
  
-   **Sincronización**, lo que indica si la API expone la capacidad para realizar la sincronización entre los subprocesos.  
  
-   **ExternalProcessMgmt**, lo que indica si la API expone una manera de controlar el proceso de host.  
  
 Al proporcionar estos atributos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especifica una lista de los HPA que no se permiten en el entorno hospedado a través de la seguridad de acceso del código (CAS). Los requisitos de CAS se especifican mediante uno de tres [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de permisos: **seguro**, **EXTERNAL_ACCESS**, o **UNSAFE**. Se especifica uno de estos tres niveles de seguridad cuando el ensamblado se registra en el servidor, utilizando la **CREATE ASSEMBLY** instrucción. Código que se ejecuta dentro de la **seguro** o **EXTERNAL_ACCESS** conjuntos de permisos deben evitar ciertos tipos o miembros que tienen la **System.Security.Permissions.HostProtectionAttribute** atributo aplicado. Para obtener más información, consulte [creación de un ensamblado](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md) y [restricciones del modelo de programación de integración de CLR](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md).  
  
 El **HostProtectionAttribute** no es un permiso de seguridad como una manera de mejorar la fiabilidad, en que identifica el código específico construye, tipos o métodos, que puede no estar permitidas en el host. El uso de la **HostProtectionAttribute** exige un modelo de programación que ayuda a proteger la estabilidad del host.  
  
## <a name="host-protection-attributes"></a>Atributos de protección del host  
 Los HPA identifican los tipos o miembros que no se ajustan al modelo de programación del host y representan los siguientes niveles crecientes de amenaza de confiabilidad:  
  
-   En caso contrario son favorables.  
  
-   Podrían provocar la desestabilización del código de usuario administrado por servidor.  
  
-   Podría provocar la desestabilización del propio proceso de servidor.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se permite el uso de un tipo o miembro que tiene un **HostProtectionAttribute** que especifica un **System.Security.Permissions.HostProtectionResource** enumeración con un valor de  **ExternalProcessMgmt**, **ExternalThreading**, **MayLeakOnAbort**, **SecurityInfrastructure**,  **SelfAffectingProcessMgmnt**, **SelfAffectingThreading**, **SharedState**, **sincronización**, o **delainterfazdeusuario**. De esta forma, se evita que los ensamblados llamen a miembros que habiliten el estado compartido, ejecuten la sincronización, puedan causar una pérdida de recursos al terminar o afecten la integridad de los procesos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="disallowed-types-and-members"></a>Tipos y miembros no permitidos  
 Los temas siguientes identifican los tipos y miembros cuyos **HostProtectionResource** valores no están permitidos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Las listas de estos temas se generaron a partir de los ensamblados admitidos.  Para obtener más información, consulte [bibliotecas de .NET Framework admite](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
## <a name="in-this-section"></a>En esta sección  
 [Miembros de Microsoft.VisualBasic.dll y tipos no permitidos](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)  
 Enumera los tipos y miembros de Microsoft.VisualBasic.dll cuyos valores de HPA no se permiten.  
  
 [Tipos y miembros en mscorlib.dll denegados](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)  
 Enumera los tipos y miembros en mscorlib.dll cuyos valores HPA no se permiten.  
  
 [Tipos y miembros en System.dll denegados](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)  
 Enumera los tipos y miembros en System.dll cuyos valores HPA no se permiten.  
  
 [Tipos y miembros en System.Data.dll denegados](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-data-dll.md)  
 Enumera los tipos y miembros en System.Data.dll cuyos valores HPA no se permiten.  
  
 [Tipos y miembros en System.Core.dll denegados](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
 Enumera los tipos y miembros en System.Core.dll cuyos valores HPA no se permiten.  
  
## <a name="see-also"></a>Vea también  
 [Seguridad de acceso del código de integración de CLR](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Restricciones del modelo de programación de integración de CLR](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Creación de un ensamblado](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  

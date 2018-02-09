---
title: "Seguridad de la integración de CLR | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- security [CLR integration]
- authorization [CLR integration]
- common language runtime [SQL Server], security
- database objects [CLR integration], security
ms.assetid: 05d7a471-c5d5-4730-b903-e4edc8157bb4
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bc6038395a2a4206095da0d7a2a3ecf8ab5f72cc
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="clr-integration-security"></a>Seguridad de la integración CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
El modelo de seguridad de la integración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Common Language Runtime (CLR) administra y protege el acceso entre los distintos tipos de objetos que se ejecutan dentro de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], tanto objetos CLR como objetos no CLR. Es posible llamar a estos objetos mediante una instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] u otro objeto CLR que se ejecute en el servidor. Las llamadas entre objetos reciben el nombre de vínculos. Los tipos de comprobaciones de seguridad que se realizan en estos objetos dependen de los tipos de vínculos implicados.  
  
 El modelo de seguridad de la integración CLR tiene estos objetivos:  
  
-   De forma predeterminada, el hecho de ejecutar código de usuario administrado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no debería poner en peligro la integridad y la estabilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La realización de operaciones que podrían poner en peligro la estabilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debería protegerse mediante los permisos de alto nivel pertinentes.  
  
-   El código de usuario administrado no debería obtener un acceso no autorizado a los datos del usuario ni a ningún otro código de usuario de la base de datos. El código definido por el usuario debería ejecutarse bajo el contexto de seguridad de la sesión del usuario que lo invocó y con los privilegios adecuados para ese contexto de seguridad.  
  
-   Debería haber controles que restringiesen el acceso del código de usuario a cualquier recurso situado fuera del servidor, y utilizarlo única y exclusivamente para el acceso a datos local y la realización de cálculos.  
  
-   El código definido por el usuario no debería poder obtener un acceso no autorizado a los recursos del sistema por el hecho de ejecutarse en el proceso de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Ahora se integra el modelo de seguridad basada en usuario de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con el modelo de seguridad basada en el acceso del código de CLR. Algunas de las ventajas que este enfoque combinado ofrece para la seguridad se describen en esta sección.  
  
 En la siguiente tabla se muestran los temas de esta sección.  
  
 [Seguridad de acceso del código de integración CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)  
 Describe el modelo de seguridad de acceso del código (CAS) para el código administrado.  
  
 [Atributos de protección del host y programación de la integración CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)  
 Ofrece información sobre los valores del atributo de protección de host (HPA) que no se permiten en los ensamblados SAFE y EXTERNAL_ACCESS.  
  
 [Vínculos de seguridad de la integración de CLR](http://msdn.microsoft.com/library/168efd01-d12e-4bdf-a1b3-0b5c76474eaf)  
 Describe la forma en que los fragmentos de código del usuario pueden llamarse entre sí en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Suplantación y seguridad de la integración de CLR](http://msdn.microsoft.com/library/1495a7af-2248-4cee-afdb-9269fb3a7774)  
 Explica la forma en que el código administrado obtiene acceso a los recursos externos utilizando la suplantación.  
  
 [Permitir parcialmente llamadores de confianza](http://msdn.microsoft.com/library/20b0248f-36da-4fc3-97d2-3789fcf6e084)  
 Indica los problemas que surgen cuando un método administrado invoca a un método en una clase incluida dentro de otro ensamblado.  
  
 [Dominios de aplicación y seguridad de la integración de CLR](http://msdn.microsoft.com/library/54ee904e-e21a-4ee7-b4ad-a6f6f71bd473)  
 Describe la forma en que los ensamblados se cargan en los dominios de aplicación.  
  
## <a name="see-also"></a>Vea también  
 [Administrar ensamblados de integración de CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)  
  
  

---
title: Seguridad de la integración de CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- security [CLR integration]
- authorization [CLR integration]
- common language runtime [SQL Server], security
- database objects [CLR integration], security
ms.assetid: 05d7a471-c5d5-4730-b903-e4edc8157bb4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 12ca3fcb00122313c1d1e4aae8b64733be9140c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62918997"
---
# <a name="clr-integration-security"></a>Seguridad de la integración CLR
  El modelo de seguridad de la [!INCLUDE[ssNoVersion](../../../includes/dnprdnshort-md.md)] common language runtime (CLR) administra y protege el acceso entre diferentes tipos de objetos CLR y que no son CLR que se ejecutan en [!INCLUDE[ssNoVersion](../../../includes/tsql-md.md)] instrucción u otro objeto CLR que se ejecutan en el servidor. Las llamadas entre objetos reciben el nombre de vínculos. Los tipos de comprobaciones de seguridad que se realizan en estos objetos dependen de los tipos de vínculos implicados.  
  
 El modelo de seguridad de la integración CLR tiene estos objetivos:  
  
-   De forma predeterminada, ejecutar código de usuario administrado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La realización de operaciones que podrían poner en peligro la estabilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debería protegerse mediante los permisos de alto nivel pertinentes.  
  
-   El código de usuario administrado no debería obtener un acceso no autorizado a los datos del usuario ni a ningún otro código de usuario de la base de datos. El código definido por el usuario debería ejecutarse bajo el contexto de seguridad de la sesión del usuario que lo invocó y con los privilegios adecuados para ese contexto de seguridad.  
  
-   Debería haber controles que restringiesen el acceso del código de usuario a cualquier recurso situado fuera del servidor, y utilizarlo única y exclusivamente para el acceso a datos local y la realización de cálculos.  
  
-   El código definido por el usuario no debería poder obtener un acceso no autorizado a los recursos del sistema por el hecho de ejecutarse en el proceso de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con el modelo de seguridad basada en el acceso del código de CLR. Algunas de las ventajas que este enfoque combinado ofrece para la seguridad se describen en esta sección.  
  
 En la siguiente tabla se muestran los temas de esta sección.  
  
 [Seguridad de acceso del código de integración CLR](clr-integration-code-access-security.md)  
 Describe el modelo de seguridad de acceso del código (CAS) para el código administrado.  
  
 [Atributos de protección del host y programación de la integración CLR](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)  
 Ofrece información sobre los valores del atributo de protección de host (HPA) que no se permiten en los ensamblados SAFE y EXTERNAL_ACCESS.  
  
 [Vínculos en el ámbito de seguridad de la integración CLR](../../../database-engine/dev-guide/links-in-clr-integration-security.md)  
 Describe la forma en que los fragmentos de código del usuario pueden llamarse entre sí en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Suplantación y seguridad de la integración CLR](../../../database-engine/dev-guide/impersonation-and-clr-integration-security.md)  
 Explica la forma en que el código administrado obtiene acceso a los recursos externos utilizando la suplantación.  
  
 [Permitir llamadores de confianza parcial](../../../database-engine/dev-guide/allowing-partially-trusted-callers.md)  
 Indica los problemas que surgen cuando un método administrado invoca a un método en una clase incluida dentro de otro ensamblado.  
  
 [Dominios de aplicación y seguridad de la integración CLR](../../../database-engine/dev-guide/application-domains-and-clr-integration-security.md)  
 Describe la forma en que los ensamblados se cargan en los dominios de aplicación.  
  
## <a name="see-also"></a>Vea también  
 [Administrar ensamblados de integración CLR](../assemblies/managing-clr-integration-assemblies.md)  
  
  

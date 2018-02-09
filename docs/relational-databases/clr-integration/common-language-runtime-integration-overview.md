---
title: "Descripción de la integración Common Language Runtime (CLR) | Documentos de Microsoft"
ms.custom: 
ms.date: 06/20/2017
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
- managed code [SQL Server]
- common language runtime [SQL Server], about CLR integration
- cross-language integration
- integrating CLR [SQL Server]
- .NET Framework [SQL Server], common language runtime
- code access security [CLR integration]
- managed code [SQL Server], CLR integration
ms.assetid: 7be9e644-36a2-48fc-9206-faf59fdff4d7
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e6c8c992a82ba88b6e3dd2d123474ad043580302
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="common-language-runtime-integration-overview"></a>Descripción de la integración de tiempo de ejecución de lenguaje común
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ahora ofrece la integración del componente common language runtime (CLR) de .NET Framework para [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. El CLR proporciona código administrado con servicios como, por ejemplo, integración entre idiomas, seguridad de acceso del código, administración de la vigencia del objeto y compatibilidad con la depuración y la creación de perfiles. Para los usuarios y programadores de aplicaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la integración CLR significa que ahora se pueden escribir procedimientos almacenados, desencadenadores, tipos definidos por el usuario, funciones definidas por el usuario (escalares y con valores de tabla) y funciones de agregado definidas por el usuario con cualquier lenguaje .NET Framework, incluidos [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET y [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye .NET Framework versión 4 preinstalado.  

>  [!WARNING]
>  CLR usa la seguridad de acceso del código (CAS) de .NET Framework, que ya no se admite como un límite de seguridad. Un ensamblado CLR creado con la opción `PERMISSION_SET = SAFE` puede tener acceso a los recursos externos del sistema, llamar a código no administrado y adquirir privilegios sysadmin. A partir de [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)], se incluye una opción de `sp_configure` denominada `clr strict security` para mejorar la seguridad de los ensamblados CLR. La opción `clr strict security` está habilitada de forma predeterminada y trata los ensamblados `SAFE` y `EXTERNAL_ACCESS` como si estuvieran marcados con `UNSAFE`. La opción `clr strict security` se puede deshabilitar para permitir la compatibilidad con versiones anteriores, pero no se recomienda hacerlo. Microsoft recomienda que todos los ensamblados estén firmados con un certificado o clave asimétrica con el correspondiente inicio de sesión que tenga concedido el permiso `UNSAFE ASSEMBLY` en la base de datos maestra. Para obtener más información, vea [CLR strict security](../../database-engine/configure-windows/clr-strict-security.md). Los administradores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también pueden agregar ensamblados a una lista de los ensamblados en los que el motor de base de datos debe confiar. Para más información, vea [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md).

 Entre las ventajas principales de esta integración se encuentran las siguientes:  
  
-   **Un mejor modelo de programación.** Los lenguajes de .NET Framework son en muchos aspectos más ricos que Transact-SQL, ya que proporcionan construcciones y funciones que antes no estaban disponibles para los desarrolladores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los programadores también pueden aprovechar el potencial de la Biblioteca de .NET Framework, que proporciona un amplio conjunto de clases que se pueden utilizar de forma rápida y eficaz para solucionar problemas de programación.  
  
-   **Seguridad mejorada y seguridad.** El código administrado se ejecuta en un entorno de Common Language Runtime, hospedado por el motor de base de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lo aprovecha para proporcionar una alternativa más segura a los procedimientos almacenados extendidos disponibles en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Capacidad para definir tipos de datos y funciones de agregado.** Los tipos y agregados definidos por el usuario son dos nuevos objetos de base de datos administrados que amplían las capacidades de almacenamiento y consulta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Desarrollo optimizado a través de un entorno normalizado.** El desarrollo de base de datos está integrado en versiones futuras del entorno de desarrollo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio .NET. Los programadores utilizan las mismas herramientas para desarrollar y depurar objetos de base de datos y scripts que las que usan para escribir componentes y servicios de .NET Framework de nivel medio o nivel de cliente.  
  
-   **Potencial para mejorar el rendimiento y escalabilidad.** En muchas situaciones, los modelos de compilación y ejecución de .NET Framework proporcionan un rendimiento mejorado con respecto a Transact-SQL.  
  
 En la siguiente tabla se muestran los temas de esta sección.  
  
 [Información general de la integración CLR](../../relational-databases/clr-integration/clr-integration-overview.md)  
 Describe los tipos de objetos que pueden generarse utilizando la integración con CLR y revisa los requisitos para generar objetos de base de datos mediante la integración con CLR.  
  
 [Novedades de la integración CLR](../../relational-databases/clr-integration/clr-integration-what-s-new.md)  
 Describe las nuevas características de esta versión.  
  
 [Arquitectura de integración de CLR](http://msdn.microsoft.com/library/05e4b872-3d21-46de-b4d5-739b5f2a0cf9)  
 Describe los objetivos de diseño de la integración con CLR.  
  
 [Habilitar la integración con CLR](../../relational-databases/clr-integration/clr-integration-enabling.md)  
 Describe cómo habilitar la integración con CLR.  
  
## <a name="see-also"></a>Vea también  
 [Instalar .NET Framework](http://technet.microsoft.com/library/ms166014\(v=SQL.105\).aspx)   
 [Rendimiento de la integración CLR](../../relational-databases/clr-integration/clr-integration-architecture-performance.md)  
  
  

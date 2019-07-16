---
title: Descripción de integración de Common Language Runtime (CLR) | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 922489d1145204a4ae5d2dcf8e483149f1b11bcf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068461"
---
# <a name="common-language-runtime-integration"></a>Integración con Common Language Runtime
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-index) le permiten implementar algunas de las funcionalidades de uso de lenguajes de .net mediante la integración de common language runtime (CLR) nativo como los módulos (procedimientos, funciones de servidor SQL Server y desencadenadores). El CLR proporciona código administrado con servicios como, por ejemplo, integración entre idiomas, seguridad de acceso del código, administración de la vigencia del objeto y compatibilidad con la depuración y la creación de perfiles. Para los usuarios y programadores de aplicaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la integración CLR significa que ahora se pueden escribir procedimientos almacenados, desencadenadores, tipos definidos por el usuario, funciones definidas por el usuario (escalares y con valores de tabla) y funciones de agregado definidas por el usuario con cualquier lenguaje .NET Framework, incluidos [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET y [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye .NET Framework versión 4 preinstalado.  

> [!WARNING]
>  CLR usa la seguridad de acceso del código (CAS) de .NET Framework, que ya no se admite como un límite de seguridad. Un ensamblado CLR creado con la opción `PERMISSION_SET = SAFE` puede tener acceso a los recursos externos del sistema, llamar a código no administrado y adquirir privilegios sysadmin. A partir de [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)], se incluye una opción de `sp_configure` denominada `clr strict security` para mejorar la seguridad de los ensamblados CLR. La opción `clr strict security` está habilitada de forma predeterminada y trata los ensamblados `SAFE` y `EXTERNAL_ACCESS` como si estuvieran marcados con `UNSAFE`. La opción `clr strict security` se puede deshabilitar para permitir la compatibilidad con versiones anteriores, pero no se recomienda hacerlo. Microsoft recomienda que todos los ensamblados estén firmados con un certificado o clave asimétrica con el correspondiente inicio de sesión que tenga concedido el permiso `UNSAFE ASSEMBLY` en la base de datos maestra. Para obtener más información, vea [CLR strict security](../../database-engine/configure-windows/clr-strict-security.md). Los administradores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también pueden agregar ensamblados a una lista de los ensamblados en los que el motor de base de datos debe confiar. Para más información, vea [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md).

## <a name="when-to-use-clr-modules"></a>¿Cuándo usar módulos CLR?

Integración de CLR le permite implementar características complejas que están disponibles en .net Framework como expresiones regulares, el código para tener acceso a recursos externos (servidores, servicios web, bases de datos), cifrado personalizado, etcetera. Algunas de las ventajas de la integración de CLR del lado del servidor son:
  
-   **Un mejor modelo de programación.** Los lenguajes de .NET Framework son en muchos aspectos más ricos que Transact-SQL, ya que proporcionan construcciones y funciones que antes no estaban disponibles para los desarrolladores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los programadores también pueden aprovechar el potencial de la Biblioteca de .NET Framework, que proporciona un amplio conjunto de clases que se pueden utilizar de forma rápida y eficaz para solucionar problemas de programación.  
  
-   **Seguridad y protección mejorada.** El código administrado se ejecuta en un entorno de Common Language Runtime, hospedado por el motor de base de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lo aprovecha para proporcionar una alternativa más segura a los procedimientos almacenados extendidos disponibles en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Capacidad para definir tipos de datos y funciones de agregado.** Los tipos y agregados definidos por el usuario son dos nuevos objetos de base de datos administrados que amplían las capacidades de almacenamiento y consulta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Desarrollo mejorado gracias a un entorno normalizado.** El desarrollo de base de datos está integrado en versiones futuras del entorno de desarrollo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio .NET. Los programadores utilizan las mismas herramientas para desarrollar y depurar objetos de base de datos y scripts que las que usan para escribir componentes y servicios de .NET Framework de nivel medio o nivel de cliente.  
  
-   **Potencial para mejorar el rendimiento y escalabilidad.** En muchas situaciones, los modelos de compilación y ejecución de .NET Framework proporcionan un rendimiento mejorado con respecto a Transact-SQL.  
  
 En la siguiente tabla se muestran los temas de esta sección.  
  
 [Información general de la integración CLR](../../relational-databases/clr-integration/clr-integration-overview.md)  
 Describe los tipos de objetos que pueden generarse utilizando la integración con CLR y revisa los requisitos para generar objetos de base de datos mediante la integración con CLR.  
  
 [Novedades de la integración CLR](../../relational-databases/clr-integration/clr-integration-what-s-new.md)  
 Describe las nuevas características de esta versión.  
  
 [Arquitectura de integración CLR](https://msdn.microsoft.com/library/05e4b872-3d21-46de-b4d5-739b5f2a0cf9)  
 Describe los objetivos de diseño de la integración con CLR.  
  
 [Habilitar la integración con CLR](../../relational-databases/clr-integration/clr-integration-enabling.md)  
 Describe cómo habilitar la integración con CLR.  
  
## <a name="see-also"></a>Vea también  
 [Instalar .NET Framework](https://technet.microsoft.com/library/ms166014\(v=SQL.105\).aspx) ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo)   
 [Rendimiento de la integración CLR](../../relational-databases/clr-integration/clr-integration-architecture-performance.md)  
  
  

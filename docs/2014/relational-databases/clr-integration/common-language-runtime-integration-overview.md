---
title: Descripción de integración de Common Language Runtime (CLR) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: a7764c6e8e45b56e43e592e70b1c85b8d4744b69
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53354852"
---
# <a name="common-language-runtime-clr-integration-overview"></a>Información general sobre integración CLR (Common Language Runtime)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incorpora ahora la integración del componente Common Language Runtime (CLR) de .NET Framework para [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. El CLR proporciona código administrado con servicios como, por ejemplo, integración entre idiomas, seguridad de acceso del código, administración de la vigencia del objeto y compatibilidad con la depuración y la creación de perfiles. Para los usuarios y programadores de aplicaciones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la integración CLR significa que ahora se pueden escribir procedimientos almacenados, desencadenadores, tipos definidos por el usuario, funciones definidas por el usuario (escalares y con valores de tabla) y funciones de agregado definidas por el usuario con cualquier lenguaje .NET Framework, incluidos [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET y [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incluye .NET Framework versión 4 preinstalado.  
  
 Entre las ventajas principales de esta integración se encuentran las siguientes:  
  
-   **Un mejor modelo de programación.** Los lenguajes de .NET Framework son en muchos aspectos más ricos que Transact-SQL, ya que proporcionan construcciones y funciones que antes no estaban disponibles para los desarrolladores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los programadores también pueden aprovechar el potencial de la Biblioteca de .NET Framework, que proporciona un amplio conjunto de clases que se pueden utilizar de forma rápida y eficaz para solucionar problemas de programación.  
  
-   **Seguridad y protección mejorada.** El código administrado se ejecuta en un entorno de Common Language Runtime, hospedado por el motor de base de datos. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] lo aprovecha para proporcionar una alternativa más segura a los procedimientos almacenados extendidos disponibles en versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   **Capacidad para definir tipos de datos y funciones de agregado.** Los tipos y agregados definidos por el usuario son dos nuevos objetos de base de datos administrados que amplían las capacidades de almacenamiento y consulta de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   **Desarrollo mejorado gracias a un entorno normalizado.** El desarrollo de base de datos está integrado en versiones futuras del entorno de desarrollo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio .NET. Los programadores utilizan las mismas herramientas para desarrollar y depurar objetos de base de datos y scripts que las que usan para escribir componentes y servicios de .NET Framework de nivel medio o nivel de cliente.  
  
-   **Potencial para mejorar el rendimiento y escalabilidad.** En muchas situaciones, los modelos de compilación y ejecución de .NET Framework proporcionan un rendimiento mejorado con respecto a Transact-SQL.  
  
 En la siguiente tabla se muestran los temas de esta sección.  
  
 [Información general de la integración CLR](clr-integration-overview.md)  
 Describe los tipos de objetos que pueden generarse utilizando la integración con CLR y revisa los requisitos para generar objetos de base de datos mediante la integración con CLR.  
  
 [Novedades de la integración CLR](clr-integration-what-s-new.md)  
 Describe las nuevas características de esta versión.  
  
 [Arquitectura de integración CLR](../../database-engine/dev-guide/architecture-of-clr-integration.md)  
 Describe los objetivos de diseño de la integración con CLR.  
  
 [Habilitar la integración con CLR](clr-integration-enabling.md)  
 Describe cómo habilitar la integración con CLR.  
  
## <a name="see-also"></a>Vea también  
 [Instalar .NET Framework](https://technet.microsoft.com/library/ms166014\(v=SQL.105\).aspx)   
 [Rendimiento de la integración CLR](clr-integration-architecture-performance.md)  
  
  

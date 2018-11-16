---
title: Conceptos de programación integración de Common Language Runtime (CLR) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- CLR [SQL Server] See common language runtime [SQL Server]
- Database Engine [SQL Server], .NET Framework
- .NET Framework [SQL Server], Database Engine programming
- common language runtime [SQL Server]
- .NET Framework [SQL Server]
ms.assetid: 951bf851-3e6e-4361-ae6a-2bcd5b837ebd
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 44dea69fde76f34fea7a6a4f5c3319d1b1a1772a
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51675744"
---
# <a name="common-language-runtime-clr-integration-programming-concepts"></a>Conceptos de programación en el ámbito de la integración de Common Language Runtime (CLR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incorpora la integración del componente Common Language Runtime (CLR) de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework para Windows. Esto significa que ahora puede escribir procedimientos almacenados, desencadenadores, tipos definidos por el usuario, funciones definidas por el usuario, agregados definidos por el usuario, así como funciones con valores de tabla de transmisión por secuencias mediante cualquier lenguaje de .NET Framework, incluidos [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET y [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#.  
  
 El espacio de nombres Microsoft.SqlServer.Server incluye funcionalidad básica para la programación CLR en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sin embargo, el espacio de nombres Microsoft.SqlServer.Server se documenta en el SDK de .NET Framework. Esta documentación no está incluida en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  De forma predeterminada, .NET Framework se instala con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pero no es así para .NET Framework SDK. Sin el SDK instalado en su equipo e incluido en la colección de Libros en pantalla, no funcionan los vínculos al contenido de SDK de esta sección. Instale .NET Framework SDK. Una vez instalado, agregue el SDK a la colección de libros en pantalla y la tabla de contenido siguiendo las instrucciones de [instalar el SDK de .NET Framework](https://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx).  
  
> [!NOTE]  
>  Funcionalidad CLR, como las funciones de usuario CLR, son *no* compatibles con Azure SQL Database.  
  
 En la siguiente tabla se muestran los temas de esta sección.  
  
 [Common Language Runtime &#40;CLR&#41; Introducción a la integración](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)  
 Proporciona una breve introducción a CLR y describe cómo y por qué se ha utilizado esta tecnología en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Describe las ventajas de usar CLR para crear objetos de base de datos.  
  
 [Ensamblados &#40;motor de la base de datos&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)  
 Describe cómo se utilizan los ensamblados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para implementar funciones, procedimientos almacenados, desencadenadores, agregados y tipos definidos por el usuario, escritos en uno de los lenguajes de código administrado (no en [!INCLUDE[msCoName](../../includes/msconame-md.md)]) y que se hospedan en Common Language Runtime (CLR) de [!INCLUDE[tsql](../../includes/tsql-md.md)] .NET Framework.  
  
 [Creación de objetos de base de datos con Common Language Runtime &#40;CLR&#41; integración](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)  
 Describe los tipos de objetos que pueden estar generados mediante CLR y revisa los requisitos para generar objetos de base de datos de CLR.  
  
 [Acceso a datos de objetos de base de datos de CLR](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
 Describe cómo una rutina CLR puede tener acceso a los datos almacenados en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Seguridad de la integración CLR](../../relational-databases/clr-integration/security/clr-integration-security.md)  
 Describe el modelo de seguridad de la integración CLR.  
  
 [Depurar objetos de base de datos CLR](../../relational-databases/clr-integration/debugging-clr-database-objects.md)  
 Describe las limitaciones y los requisitos para depurar los objetos de la base de datos de CLR.  
  
 [Implementar objetos de base de datos CLR](../../relational-databases/clr-integration/deploying-clr-database-objects.md)  
 Describe los ensamblados de implementación a servidores de producción.  
  
 [Administrar ensamblados de integración CLR](../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)  
 Describe cómo crear y quitar los ensamblados de integración CLR.  
  
 [Supervisar y solucionar problemas de objetos de base de datos administrados](../../relational-databases/clr-integration/monitoring-and-troubleshooting-managed-database-objects.md)  
 Se proporciona información sobre las herramientas que se pueden utilizar para supervisar y solucionar problemas de los objetos de base de datos administrados y ensamblados que se ejecutan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Escenarios de uso y ejemplos para la integración de Common Language Runtime &#40;CLR&#41;](https://msdn.microsoft.com/library/33aac25f-abb4-4f29-af88-4a0dacd80ae7)  
 Describe escenarios de uso y ejemplos de código que usan objetos CLR.  
  
## <a name="see-also"></a>Vea también  
 [Los ensamblados &#40;motor de base de datos&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [Instalar el SDK de .NET Framework](https://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx)  
  
  

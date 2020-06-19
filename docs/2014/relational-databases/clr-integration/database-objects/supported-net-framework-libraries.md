---
title: Bibliotecas de .NET Framework compatibles | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], .NET Framework libraries
- .NET Framework [CLR Integration]
ms.assetid: 417544ff-c25c-496e-add4-2f278f8a4911
author: rothja
ms.author: jroth
ms.openlocfilehash: 0db38e8bf21d56a0fcd35208920b9ee24b583062
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84953481"
---
# <a name="supported-net-framework-libraries"></a>Bibliotecas de .NET Framework admitidas
  Con Common Language Runtime (CLR) hospedado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], puede crear procedimientos almacenados, desencadenadores, funciones definidas por el usuario, tipos definidos por el usuario y agregados definidos por el usuario en código administrado. Con la funcionalidad de las bibliotecas de clases de.NET Framework, tiene acceso a clases pregeneradas que proporcionan funcionalidad para la manipulación de cadenas, operaciones matemáticas avanzadas, acceso a archivos, criptografía, etc. Se puede tener acceso a estas clases desde cualquier procedimiento almacenado administrado, tipo definido por el usuario, desencadenador, función definida por el usuario o agregado definido por el usuario.  
  
> [!NOTE]  
>  Si el servicio o actualiza los ensamblados no compatibles en la caché de ensamblados global (GAC), el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Si un ensamblado existe en una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] integración CLR. Si mantiene o actualiza cualquier ensamblado en la GAC que también esté registrado en la base de datos, incluidos los ensamblados de .NET Framework no compatibles, asegúrese de que también mantiene o actualiza la copia del ensamblado en las bases de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con la instrucción `ALTER ASSEMBLY`. Para obtener más información, vea el [artículo 949080 de Knowledge Base](https://support.microsoft.com/kb/949080).  
  
## <a name="supported-libraries"></a>Bibliotecas compatibles  
 A partir de [!INCLUDE[ssVersion2005](../../../includes/ssnoversion-md.md)] tiene una lista de bibliotecas de .NET Framework compatibles, que se han probado para garantizar que cumplen con los estándares de seguridad y confiabilidad para la interacción con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] las carga directamente desde la caché de ensamblados global (GAC).  
  
 Las bibliotecas/espacios de nombres que admite la integración CLR en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] son:  
  
-   CustomMarshalers  
  
-   Microsoft.VisualBasic  
  
-   Microsoft.VisualC  
  
-   mscorlib  
  
-   Sistema  
  
-   System.Configuration  
  
-   System.Data  
  
-   System.Data.OracleClient  
  
-   System.Data.SqlXml  
  
-   System.Deployment  
  
-   System.Security  
  
-   System.Transactions  
  
-   System.Web.Services  
  
-   System.Xml  
  
-   System.Core.dll  
  
-   System.Xml.Linq.dll  
  
## <a name="unsupported-libraries"></a>Bibliotecas no compatibles  
 También se puede llamar a bibliotecas no compatibles desde los procedimientos almacenados administrados, desencadenadores, funciones definidas por el usuario, tipos definidos por el usuario y agregados definidos por el usuario. La biblioteca no compatible se debe registrar previamente en la base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], mediante la instrucción `CREATE ASSEMBLY`, antes de utilizarla en el código. Las bibliotecas no compatibles que se registren y se ejecuten en el servidor se deben revisar y probar para garantizar la seguridad y la confiabilidad.  
  
 Por ejemplo, el espacio de nombres `System.DirectoryServices` no se admite. Debe registrar el ensamblado System.DirectoryServices.dll con permisos `UNSAFE` antes de llamarlo desde el código. El permiso `UNSAFE` es necesario porque las clases del espacio de nombres `System.DirectoryServices` no cumplen los requisitos de `SAFE` ni `EXTERNAL_ACCESS`. Para obtener más información, vea restricciones del modelo de programación de la [integración CLR](clr-integration-programming-model-restrictions.md) y [seguridad de acceso del código de integración CLR](../security/clr-integration-code-access-security.md).  
  
## <a name="see-also"></a>Consulte también  
 [Crear un ensamblado](../assemblies/creating-an-assembly.md)   
 [Seguridad de acceso del código de integración CLR](../security/clr-integration-code-access-security.md)   
 [Restricciones del modelo de programación de la integración CLR](clr-integration-programming-model-restrictions.md)  
  
  

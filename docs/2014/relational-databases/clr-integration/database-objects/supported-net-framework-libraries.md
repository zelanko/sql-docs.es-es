---
title: Admite bibliotecas de .NET Framework | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: c2518404830577839bce3e84c4eac9b76c850cd3
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53367970"
---
# <a name="supported-net-framework-libraries"></a>Bibliotecas de .NET Framework admitidas
  Con Common Language Runtime (CLR) hospedado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], puede crear procedimientos almacenados, desencadenadores, funciones definidas por el usuario, tipos definidos por el usuario y agregados definidos por el usuario en código administrado. Con la funcionalidad de las bibliotecas de clases de.NET Framework, tiene acceso a clases pregeneradas que proporcionan funcionalidad para la manipulación de cadenas, operaciones matemáticas avanzadas, acceso a archivos, criptografía, etc. Se puede tener acceso a estas clases desde cualquier procedimiento almacenado administrado, tipo definido por el usuario, desencadenador, función definida por el usuario o agregado definido por el usuario.  
  
> [!NOTE]  
>  Si mantiene o actualiza ensamblados no compatibles en la caché global de ensamblados (GAC), su [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si existe un ensamblado en un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] integración CLR. Si mantiene o actualiza cualquier ensamblado en la GAC que también esté registrado en la base de datos, incluidos los ensamblados de .NET Framework no compatibles, asegúrese de que también mantiene o actualiza la copia del ensamblado en las bases de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con la instrucción `ALTER ASSEMBLY`. Para obtener más información, consulte [artículo 949080 de Knowledge Base](https://support.microsoft.com/kb/949080).  
  
## <a name="supported-libraries"></a>Bibliotecas compatibles  
 A partir [!INCLUDE[ssVersion2005](../../../includes/ssnoversion-md.md)] tiene una lista de bibliotecas de .NET Framework compatibles, que se han probado para garantizar que cumplen los estándares de confiabilidad y seguridad para la interacción con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] carga directamente desde la Global caché ensamblados (GAC).  
  
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
  
 Por ejemplo, el espacio de nombres `System.DirectoryServices` no se admite. Debe registrar el ensamblado System.DirectoryServices.dll con permisos `UNSAFE` antes de llamarlo desde el código. El permiso `UNSAFE` es necesario porque las clases del espacio de nombres `System.DirectoryServices` no cumplen los requisitos de `SAFE` ni `EXTERNAL_ACCESS`. Para obtener más información, consulte [restricciones del modelo de programación de integración de CLR](clr-integration-programming-model-restrictions.md) y [CLR Integration Code Access Security](../security/clr-integration-code-access-security.md).  
  
## <a name="see-also"></a>Vea también  
 [Creación de un ensamblado](../assemblies/creating-an-assembly.md)   
 [Seguridad de acceso del código de integración de CLR](../security/clr-integration-code-access-security.md)   
 [Restricciones del modelo de programación de la integración CLR](clr-integration-programming-model-restrictions.md)  
  
  

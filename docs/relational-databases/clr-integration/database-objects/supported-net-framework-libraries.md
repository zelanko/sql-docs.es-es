---
title: Admite las bibliotecas de .NET Framework | Documentos de Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], .NET Framework libraries
- .NET Framework [CLR Integration]
ms.assetid: 417544ff-c25c-496e-add4-2f278f8a4911
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b6153914ef43333ad2feefb1dd428974c15eb83b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="supported-net-framework-libraries"></a>Bibliotecas de .NET Framework admitidas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Con common language runtime (CLR) hospedado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], puede crear procedimientos almacenados, desencadenadores, funciones definidas por el usuario, tipos definidos por el usuario y agregados definidos por el usuario en código administrado. Con la funcionalidad de las bibliotecas de clases de.NET Framework, tiene acceso a clases pregeneradas que proporcionan funcionalidad para la manipulación de cadenas, operaciones matemáticas avanzadas, acceso a archivos, criptografía, etc. Se puede tener acceso a estas clases desde cualquier procedimiento almacenado administrado, tipo definido por el usuario, desencadenador, función definida por el usuario o agregado definido por el usuario.  
  
> [!NOTE]  
>  Si mantiene o actualiza ensamblados no compatibles en la caché global de ensamblados (GAC), la aplicación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] podría dejar de funcionar. Esto se debe a que el mantenimiento o la actualización de bibliotecas en la GAC no actualiza estos ensamblados en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si un ensamblado existe en una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y en la GAC, las dos copias del ensamblado deben coincidir exactamente. Si no coinciden, se producirá un error cuando la integración CLR de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] use el ensamblado. Si mantiene o actualiza los ensamblados en la GAC que también se registran en la base de datos, incluidos los ensamblados de .NET Framework no compatibles, asegúrese de que también mantiene o actualiza la copia del ensamblado en su [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bases de datos con la  **ALTER ASSEMBLY** instrucción. Para obtener más información, consulte [el artículo de Knowledge Base 949080](http://support.microsoft.com/kb/949080).  
  
## <a name="supported-libraries"></a>Bibliotecas compatibles  
 A partir de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incluye una lista de bibliotecas de .NET Framework compatibles probadas para garantizar que satisfacen las normas de confiabilidad y seguridad para la interacción con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Las bibliotecas compatibles no necesitan registrarse explícitamente en el servidor antes de utilizarlas en el código; [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] las carga directamente desde la caché de ensamblados global (GAC).  
  
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
 También se puede llamar a bibliotecas no compatibles desde los procedimientos almacenados administrados, desencadenadores, funciones definidas por el usuario, tipos definidos por el usuario y agregados definidos por el usuario. La biblioteca no compatible en primer lugar debe estar registrada en el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] la base de datos, utilizando la **CREATE ASSEMBLY** instrucción, antes de que se puede utilizar en el código. Las bibliotecas no compatibles que se registren y se ejecuten en el servidor se deben revisar y probar para garantizar la seguridad y la confiabilidad.  
  
 Por ejemplo, el **System.DirectoryServices** no se admite el espacio de nombres. Debe registrar el ensamblado System.DirectoryServices.dll con **UNSAFE** permisos antes de que se pueden llamar desde el código. El **UNSAFE** permiso es necesario porque las clases en el **System.DirectoryServices** espacio de nombres no cumplen los requisitos de **seguro** o  **EXTERNAL_ACCESS**. Para obtener más información, consulte [restricciones del modelo de programación de integración de CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md) y [CLR Integration Code Access Security](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md).  
  
## <a name="see-also"></a>Vea también  
 [Creación de un ensamblado](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [Seguridad de acceso del código de integración de CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Restricciones del modelo de programación de la integración CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
  
  

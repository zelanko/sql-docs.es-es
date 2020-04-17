---
title: Bibliotecas de .NET Framework admitidas ? Microsoft Docs
description: Con clr hospedado en SQL Server, puede crear mediante bibliotecas de clases de .NET Framework compatibles y bibliotecas no admitidas que se registran con una base de datos.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], .NET Framework libraries
- .NET Framework [CLR Integration]
ms.assetid: 417544ff-c25c-496e-add4-2f278f8a4911
author: rothja
ms.author: jroth
ms.openlocfilehash: 459cd091043d567b4c93555c271213d066f3989e
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487145"
---
# <a name="supported-net-framework-libraries"></a>Bibliotecas de .NET Framework admitidas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Con Common Language Runtime (CLR) hospedado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], puede crear procedimientos almacenados, desencadenadores, funciones definidas por el usuario, tipos definidos por el usuario y agregados definidos por el usuario en código administrado. Con la funcionalidad de las bibliotecas de clases de.NET Framework, tiene acceso a clases pregeneradas que proporcionan funcionalidad para la manipulación de cadenas, operaciones matemáticas avanzadas, acceso a archivos, criptografía, etc. Se puede tener acceso a estas clases desde cualquier procedimiento almacenado administrado, tipo definido por el usuario, desencadenador, función definida por el usuario o agregado definido por el usuario.  
  
> [!NOTE]  
>  Si mantiene o actualiza ensamblados no compatibles en la caché global de ensamblados (GAC), la aplicación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] podría dejar de funcionar. Esto se debe a que el mantenimiento o la actualización de bibliotecas en la GAC no actualiza estos ensamblados en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si un ensamblado existe en una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y en la GAC, las dos copias del ensamblado deben coincidir exactamente. Si no coinciden, se producirá un error cuando la integración CLR de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] use el ensamblado. Si da servicio o actualiza los ensamblados de la GAC que también están registrados en la base de datos, incluidos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] los ensamblados de .NET Framework no admitidos, asegúrese de reparar o actualizar también la copia del ensamblado dentro de las bases de datos con la instrucción **ALTER ASSEMBLY.** Para obtener más información, consulte el [artículo 949080 de Knowledge Base.](https://support.microsoft.com/kb/949080)  
  
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
 También se puede llamar a bibliotecas no compatibles desde los procedimientos almacenados administrados, desencadenadores, funciones definidas por el usuario, tipos definidos por el usuario y agregados definidos por el usuario. La biblioteca no admitida debe [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] registrarse primero en la base de datos, mediante la instrucción **CREATE ASSEMBLY,** antes de que se pueda usar en el código. Las bibliotecas no compatibles que se registren y se ejecuten en el servidor se deben revisar y probar para garantizar la seguridad y la confiabilidad.  
  
 Por ejemplo, no se admite el espacio de nombres **System.DirectoryServices.** Debe registrar el ensamblado System.DirectoryServices.dll con permisos **UNSAFE** antes de poder llamarlo desde el código. El permiso **UNSAFE** es necesario porque las clases del espacio de nombres **System.DirectoryServices** no cumplen los requisitos de **SAFE** o **EXTERNAL_ACCESS**. Para obtener más información, vea [Restricciones](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md) del modelo de programación de integración de CLR y Seguridad de acceso a código de [integración de CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md).  
  
## <a name="see-also"></a>Consulte también  
 [Creación de una Asamblea](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [Seguridad de acceso al código de integración de CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Restricciones del modelo de programación de la integración CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
  
  

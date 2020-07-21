---
title: Tipos y miembros no permitidos en System.Data.dll | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: ee5f55e9-fbef-401a-be18-a2e5873c8720
author: rothja
ms.author: jroth
ms.openlocfilehash: 6417dfbe000a3c149df8abe80d1fe3b961fc08cf
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84954272"
---
# <a name="disallowed-types-and-members-in-systemdatadll"></a>Tipos y miembros no permitidos en System.Data.dll
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la programación de Common Language Integration (CLR) no permite el uso de un tipo o miembro que tenga un `HostProtectionAttribute` que especifique una `System.Security.Permissions.HostProtectionResource` enumeración con un valor de `ExternalProcessMgmt` , `ExternalThreading` , `MayLeakOnAbort` , `SecurityInfrastructure` , `SelfAffectingProcessMgmnt` , `SelfAffectingThreading` , **SharedState**, `Synchronization` o `UI` . En la tabla siguiente se enumeran los miembros y tipos del ensamblado System.Data.dll cuyos valores de atributo de protección de host (HPA) no están permitidos.  
  
> [!NOTE]  
>  Esta lista se generó a partir de los ensamblados admitidos. Para obtener más información, consulte [supported .NET Framework Libraries](../clr-integration/database-objects/supported-net-framework-libraries.md).  
  
|Tipo o miembro|Valores de HPA|  
|--------------------|--------------------|  
|System.Data.SqlClient.SqlCommand.BeginExecuteNonQuery ()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteReader()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteXmlReader()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency..ctor()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Start()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Stop()|ExternalThreading|  
|System.Data.TypedDataSetGenerator|SharedState, Synchronization|  
|System.Xml.XmlDataDocument|Sincronización|  
  
## <a name="see-also"></a>Consulte también  
 [Atributos de protección del host y programación de la integración CLR](host-protection-attributes-and-clr-integration-programming.md)   
 [Tipos y miembros no permitidos en Microsoft.VisualBasic.dll](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [Tipos y miembros no permitidos en mscorlib.dll](disallowed-types-and-members-in-mscorlib-dll.md)   
 [Tipos y miembros no permitidos en System.dll](disallowed-types-and-members-in-system-dll.md)   
 [Tipos y miembros no permitidos en System.Core.dll](disallowed-types-and-members-in-system-core-dll.md)  
  
  

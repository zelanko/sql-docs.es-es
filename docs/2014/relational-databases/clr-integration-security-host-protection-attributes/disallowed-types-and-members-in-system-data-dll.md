---
title: No se permiten tipos y miembros en System.Data.dll | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: ee5f55e9-fbef-401a-be18-a2e5873c8720
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7c222c10fe13a422e5195970057fbb623cc960a4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108608"
---
# <a name="disallowed-types-and-members-in-systemdatadll"></a>Tipos y miembros en System.Data.dll denegados
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programación de integración (CLR) de lenguaje común no permite el uso de un tipo o miembro que tiene un `HostProtectionAttribute` que especifica un `System.Security.Permissions.HostProtectionResource` enumeración con un valor de `ExternalProcessMgmt`, `ExternalThreading`, `MayLeakOnAbort`, `SecurityInfrastructure`, `SelfAffectingProcessMgmnt`, `SelfAffectingThreading`, **SharedState**, `Synchronization`, o `UI`. En la tabla siguiente se enumeran los miembros y tipos del ensamblado System.Data.dll cuyos valores de atributo de protección de host (HPA) no están permitidos.  
  
> [!NOTE]  
>  Esta lista se generó a partir de los ensamblados admitidos. Para obtener más información, consulte [bibliotecas de .NET Framework admite](../clr-integration/database-objects/supported-net-framework-libraries.md).  
  
|Tipo o miembro|Valores de HPA|  
|--------------------|--------------------|  
|System.Data.SqlClient.SqlCommand.BeginExecuteNonQuery ()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteReader()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteXmlReader()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency..ctor()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Start()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Stop()|ExternalThreading|  
|System.Data.TypedDataSetGenerator|SharedState, Synchronization|  
|System.Xml.XmlDataDocument|Synchronization|  
  
## <a name="see-also"></a>Vea también  
 [Atributos de protección de host y programación de la integración de CLR](host-protection-attributes-and-clr-integration-programming.md)   
 [Miembros de Microsoft.VisualBasic.dll y tipos no permitidos](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [Tipos y miembros en mscorlib.dll denegados](disallowed-types-and-members-in-mscorlib-dll.md)   
 [Tipos y miembros en System.dll denegados](disallowed-types-and-members-in-system-dll.md)   
 [Tipos y miembros no permitidos en System.Core.dll](disallowed-types-and-members-in-system-core-dll.md)  
  
  
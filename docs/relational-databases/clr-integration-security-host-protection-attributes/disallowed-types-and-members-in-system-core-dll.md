---
title: No se permiten tipos y miembros en System.Core.dll | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: dcd24cd6-f4ab-42cc-9786-a1604e8a4b4e
caps.latest.revision: 11
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2097d233f02fc5bf7b0cefbfc480cd4b4d795f91
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="disallowed-types-and-members-in-systemcoredll"></a>Tipos y miembros no permitidos en System.Core.dll
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programación de integración (CLR) de lenguaje común no permite el uso de un tipo o miembro que tiene un **HostProtectionAttribute** que especifica un **System.Security.Permissions.HostProtectionResource** enumeración con un valor de **ExternalProcessMgmt**, **ExternalThreading**, **MayLeakOnAbort**, **SecurityInfrastructure**, **SelfAffectingProcessMgmnt**, **SelfAffectingThreading**, **SharedState**, **sincronización**, o **Interfaz de usuario**. En la tabla siguiente se enumeran los miembros y tipos de los ensamblados System.Core.dll cuyos valores de atributo de protección de host (HPA) no están permitidos.  
  
> [!NOTE]  
>  Esta lista se generó a partir de los ensamblados admitidos. Para obtener más información, consulte [bibliotecas de .NET Framework admite](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
|Tipo o miembro|Valores de HPA|  
|--------------------|--------------------|  
|System.Diagnostics.Eventing.EventDescriptor|MayLeakOnAbort|  
|System.Diagnostics.Eventing.EventProvider|MayLeakOnAbort|  
|System.Diagnostics.Eventing.EventProviderTraceListener|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementEntityAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.WmiConfigurationAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementMemberAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementNewInstanceAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementBindAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementCreateAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementRemoveAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementEnumeratorAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementProbeAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementTaskAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementKeyAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementReferenceAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementConfigurationAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementCommitAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementNameAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.InstrumentationBaseException|MayLeakOnAbort|  
|System.Management.Instrumentation.InstrumentationException|MayLeakOnAbort|  
|System.Management.Instrumentation.InstanceNotFoundException|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventBookmark|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogConfiguration|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogLink|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogStatus|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventProperty|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogPropertySelector|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventRecord|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventKeyword|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLevel|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogRecord|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogReader|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogWatcher|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventRecordWrittenEventArgs|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogSession|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventMetadata|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventOpcode|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventTask|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogException|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogNotFoundException|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogReadingException|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogProviderDisabledException|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogInvalidDataException|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogInformation|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.ProviderMetadata|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeNCryptHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeNCryptKeyHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeNCryptProviderHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeNCryptSecretHandle|MayLeakOnAbort|  
|System.Security.Cryptography.Aes|MayLeakOnAbort|  
|System.Security.Cryptography.AesCryptoServiceProvider|MayLeakOnAbort|  
|System.Security.Cryptography.AesManaged|MayLeakOnAbort|  
|System.Security.Cryptography.CngAlgorithm|MayLeakOnAbort|  
|System.Security.Cryptography.CngAlgorithmGroup|MayLeakOnAbort|  
|System.Security.Cryptography.CngKey|MayLeakOnAbort|  
|System.Security.Cryptography.CngKeyBlobFormat|MayLeakOnAbort|  
|System.Security.Cryptography.CngKeyCreationParameters|MayLeakOnAbort|  
|System.Security.Cryptography.CngProperty|MayLeakOnAbort|  
|System.Security.Cryptography.CngPropertyCollection|MayLeakOnAbort|  
|System.Security.Cryptography.CngProvider|MayLeakOnAbort|  
|System.Security.Cryptography.CngUIPolicy|MayLeakOnAbort|  
|System.Security.Cryptography.ECDiffieHellman|MayLeakOnAbort|  
|System.Security.Cryptography.ECDiffieHellmanPublicKey|MayLeakOnAbort|  
|System.Security.Cryptography.ECDiffieHellmanCng|MayLeakOnAbort|  
|System.Security.Cryptography.ECDiffieHellmanCngPublicKey|MayLeakOnAbort|  
|System.Security.Cryptography.ECDsa|MayLeakOnAbort|  
|System.Security.Cryptography.ECDsaCng|MayLeakOnAbort|  
|System.Security.Cryptography.ManifestSignatureInformation|MayLeakOnAbort|  
|System.Security.Cryptography.ManifestSignatureInformationCollection|MayLeakOnAbort|  
|System.Security.Cryptography.MD5Cng|MayLeakOnAbort|  
|System.Security.Cryptography.SHA1Cng|MayLeakOnAbort|  
|System.Security.Cryptography.SHA256Cng|MayLeakOnAbort|  
|System.Security.Cryptography.SHA256CryptoServiceProvider|MayLeakOnAbort|  
|System.Security.Cryptography.SHA384Cng|MayLeakOnAbort|  
|System.Security.Cryptography.SHA384CryptoServiceProvider|MayLeakOnAbort|  
|System.Security.Cryptography.SHA512Cng|MayLeakOnAbort|  
|System.Security.Cryptography.SHA512CryptoServiceProvider|MayLeakOnAbort|  
|System.Security.Cryptography.StrongNameSignatureInformation|MayLeakOnAbort|  
|System.Security.Cryptography.X509Certificates.AuthenticodeSignatureInformation|MayLeakOnAbort|  
|System.Security.Cryptography.X509Certificates.TimestampInformation|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafePipeHandle|MayLeakOnAbort|  
|System.TimeZoneInfo|MayLeakOnAbort|  
|System.TimeZoneNotFoundException|MayLeakOnAbort|  
|System.InvalidTimeZoneException|MayLeakOnAbort|  
|System.Diagnostics.EventSchemaTraceListener|MayLeakOnAbort|  
|System.Diagnostics.UnescapedXmlDiagnosticData|MayLeakOnAbort|  
|System.Diagnostics.PerformanceData.CounterData|MayLeakOnAbort|  
|System.Diagnostics.PerformanceData.CounterSetInstanceCounterDataSet|MayLeakOnAbort|  
|System.Diagnostics.PerformanceData.CounterSet|MayLeakOnAbort|  
|System.Diagnostics.PerformanceData.CounterSetInstance|MayLeakOnAbort|  
|System.Collections.Generic.HashSet`1|MayLeakOnAbort|  
|System.IO.Pipes.PipeStream|MayLeakOnAbort|  
|System.IO.Pipes.AnonymousPipeServerStream|MayLeakOnAbort|  
|System.IO.Pipes.AnonymousPipeClientStream|MayLeakOnAbort|  
|System.IO.Pipes.NamedPipeServerStream|MayLeakOnAbort|  
|System.IO.Pipes.NamedPipeClientStream|MayLeakOnAbort|  
|System.IO.Pipes.PipeAccessRule|MayLeakOnAbort|  
|System.IO.Pipes.PipeAuditRule|MayLeakOnAbort|  
|System.IO.Pipes.PipeSecurity|MayLeakOnAbort|  
|System.Threading.LockRecursionException|MayLeakOnAbort|  
|System.Threading.ReaderWriterLockSlim|MayLeakOnAbort|  
  
## <a name="see-also"></a>Vea también  
 [Atributos de protección de host y programación de la integración de CLR](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Miembros de Microsoft.VisualBasic.dll y tipos no permitidos](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [Tipos y miembros en mscorlib.dll denegados](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)   
 [Tipos y miembros en System.dll denegados](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)   
 [Tipos y miembros en System.Data.dll denegados](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-data-dll.md)  
  
  

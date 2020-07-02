---
title: Tipos y miembros en Microsoft.VisualBasic.dll
description: Enumera los miembros y tipos del ensamblado de Microsoft.VisualBasic.dll cuyos valores de atributo de protección de host (HPA) no están permitidos.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: 45f55646-4bf1-4493-9f72-d1363c9a9ac6
author: rothja
ms.author: jroth
ms.openlocfilehash: 1de9adbca4c4cd0d6b71056dcb338e534f006a3e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727740"
---
# <a name="disallowed-types-and-members-in-microsoftvisualbasicdll"></a>Miembros y tipos no permitidos en Microsoft.VisualBasic.dll
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la programación de Common Language Integration (CLR) no permite el uso de un tipo o miembro que tiene un **HostProtectionAttribute** que especifica una enumeración **System. Security. Permissions. HostProtectionResource** con un valor de **ExternalProcessMgmt**, **ExternalThreading**, **MayLeakOnAbort**, **SecurityInfrastructure**, **SelfAffectingProcessMgmnt**, **SelfAffectingThreading**, **SharedState**, **Synchronization**o **UI**. En la tabla siguiente se enumeran los miembros y tipos del ensamblado de **Microsoft.VisualBasic.dll** cuyos valores de atributo de protección de host (hPa) no están permitidos.  
  
> [!NOTE]  
>  Esta lista se generó a partir de los ensamblados admitidos. Para obtener más información, consulte [supported .NET Framework Libraries](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
|**Tipo o miembro**|**Valores de HPA**|  
|------------------------|------------------------|  
|Microsoft.VisualBasic.ApplicationServices.ApplicationBase|ExternalProcessMgmt|  
|Microsoft.VisualBasic.ApplicationServices.ApplicationBase.ChangeCulture()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.ApplicationServices.ApplicationBase.get_Info()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.ApplicationServices.AssemblyInfo|ExternalProcessMgmt|  
|Microsoft.VisualBasic.ApplicationServices.BuiltInRoleConverter|SharedState|  
|Microsoft.VisualBasic.ApplicationServices.ConsoleApplicationBase|ExternalProcessMgmt|  
|Microsoft.VisualBasic.ApplicationServices.User|ExternalProcessMgmt|  
|Microsoft.VisualBasic.ApplicationServices.WebUser|ExternalProcessMgmt|  
|Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase|ExternalProcessMgmt|  
|Microsoft.VisualBasic.CompilerServices.HostServices|SharedState|  
|Microsoft.VisualBasic.CompilerServices.ProjectData.EndApp()|SelfAffectingProcessMgmt|  
|Microsoft.VisualBasic.CompilerServices.Utils.SetCultureInfo()|SelfAffectingThreading|  
|Microsoft.VisualBasic.DateAndTime.set_DateString()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.DateAndTime.set_TimeOfDay()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.DateAndTime.set_TimeString()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.DateAndTime.set_Today()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Devices.Audio|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Devices.Clock|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Devices.Computer|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Devices.ComputerInfo|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Devices.Keyboard|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Devices.Mouse|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Devices.Network|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Devices.Ports|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Devices.ServerComputer|ExternalProcessMgmt|  
|Microsoft.VisualBasic.FileIO.FileSystem|ExternalProcessMgmt|  
|Microsoft.VisualBasic.FileIO.SpecialDirectories|ExternalProcessMgmt|  
|Microsoft.VisualBasic.FileIO.TextFieldParser..ctor()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.FileSystem|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Interaction.CreateObject()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Interaction.DeleteSetting()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Interaction.GetObject()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Interaction.InputBox()|IU|  
|Microsoft.VisualBasic.Interaction.MsgBox()|IU|  
|Microsoft.VisualBasic.Logging.AspLog|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener..ctor()|ExternalProcessMgmt|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.Close()|Sincronización|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.Dispose()|Sincronización|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.Flush()|Sincronización|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.GetSupportedAttributes()|Sincronización|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.TraceData()|Sincronización|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.TraceEvent()|Sincronización|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.Write()|Sincronización|  
|Microsoft.VisualBasic.Logging.FileLogTraceListener.WriteLine()|Sincronización|  
|Microsoft.VisualBasic.Logging.Log|ExternalProcessMgmt|  
|Microsoft.VisualBasic.MyServices.ClipboardProxy|ExternalProcessMgmt|  
|Microsoft.VisualBasic.MyServices.FileSystemProxy|ExternalProcessMgmt|  
|Microsoft.VisualBasic.MyServices.RegistryProxy|ExternalProcessMgmt|  
|Microsoft.VisualBasic.MyServices.SpecialDirectoriesProxy|ExternalProcessMgmt|  
  
## <a name="see-also"></a>Consulte también  
 [Atributos de protección del host y programación de la integración CLR](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Tipos y miembros no permitidos en mscorlib.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)   
 [Tipos y miembros no permitidos en System.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)   
 [Tipos y miembros no permitidos en System.Data.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-data-dll.md)   
 [Tipos y miembros no permitidos en System.Core.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
  
  

---
title: Tipos y miembros no permitidos en mscorlib.dll | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: daf82d4b-2f6d-44ca-9148-75193321b6d5
author: rothja
ms.author: jroth
ms.openlocfilehash: cc4e42a0f900231bdd28417420cdab19b7345e66
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84954325"
---
# <a name="disallowed-types-and-members-in-mscorlibdll"></a>Miembros y tipos no permitidos en mscorlib.dll
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la programación de Common Language Integration (CLR) no permite el uso de un tipo o miembro que tenga un `HostProtectionAttribute` que especifique una `System.Security.Permissions.HostProtectionResource` enumeración con un valor de `ExternalProcessMgmt` , `ExternalThreading` , `MayLeakOnAbort` , `SecurityInfrastructure` , `SelfAffectingProcessMgmnt` , `SelfAffectingThreading` , **SharedState**, `Synchronization` o `UI` . En la tabla siguiente se enumeran los miembros y tipos del ensamblado mscorlib.dll cuyos valores de atributo de protección de host (HPA) no están permitidos.  
  
> [!NOTE]  
>  Esta lista se generó a partir de los ensamblados admitidos. Para obtener más información, consulte [supported .NET Framework Libraries](../clr-integration/database-objects/supported-net-framework-libraries.md).  
  
|Tipo o miembro|Valores de HPA|  
|--------------------|--------------------|  
|SyncStream.BeginRead()|ExternalThreading|  
|SyncStream.BeginWrite()|ExternalThreading|  
|System.Collections.ArrayList.Synchronized()|Sincronización|  
|System.Collections.Hashtable.Synchronized()|Sincronización|  
|System.Collections.Queue.Synchronized()|Sincronización|  
|System.Collections.SortedList.Synchronized()|Sincronización|  
|System.Collections.Stack.Synchronized()|Sincronización|  
|System.Console.Beep()|IU|  
|System.Console.get_Error()|IU|  
|System.Console.get_In()|IU|  
|System.Console.get_KeyAvailable()|IU|  
|System.Console.get_Out()|IU|  
|System.Console.OpenStandardError()|IU|  
|System.Console.OpenStandardInput()|IU|  
|System.Console.OpenStandardOutput()|IU|  
|System.Console.Read()|IU|  
|System.Console.ReadKey()|IU|  
|System.Console.ReadLine()|IU|  
|System.Console.SetError()|IU|  
|System.Console.SetIn()|IU|  
|System.Console.SetOut()|IU|  
|System.Console.Write()|IU|  
|System.Console.WriteLine()|IU|  
|System.Diagnostics.LogMessageEventHandler|ExternalThreading, Synchronization|  
|System.IO.FileStream.BeginRead()|ExternalThreading|  
|System.IO.FileStream.BeginWrite()|ExternalThreading|  
|System.IO.Stream.Synchronized()|Sincronización|  
|System.IO.TextReader.Synchronized()|Sincronización|  
|System.IO.TextWriter.Synchronized()|Sincronización|  
|System.Reflection.Emit.AssemblyBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.ConstructorBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.CustomAttributeBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.EnumBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.EventBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.FieldBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.MethodBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.MethodRental|MayLeakOnAbort|  
|System.Reflection.Emit.ModuleBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.PropertyBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.TypeBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.UnmanagedMarshal|MayLeakOnAbort|  
|System.Security.Principal.WindowsPrincipal|SecurityInfrastructure|  
|System.Threading.AutoResetEvent|ExternalThreading, Synchronization|  
|System.Threading.EventWaitHandle|ExternalThreading, Synchronization|  
|System.Threading.ManualResetEvent|ExternalThreading, Synchronization|  
|System.Threading.Monitor|ExternalThreading, Synchronization|  
|System.Threading.Mutex|ExternalThreading, Synchronization|  
|System.Threading.ReaderWriterLock|ExternalThreading, Synchronization|  
|System.Threading.Thread.AllocateDataSlot()|ExternalThreading, SharedState|  
|System.Threading.Thread.AllocateNamedDataSlot()|ExternalThreading, SharedState|  
|System.Threading.Thread.BeginCriticalRegion()|ExternalThreading, Synchronization|  
|System.Threading.Thread.EndCriticalRegion()|ExternalThreading, Synchronization|  
|System.Threading.Thread.FreeNamedDataSlot()|ExternalThreading, SharedState|  
|System.Threading.Thread.GetData()|ExternalThreading, SharedState|  
|System.Threading.Thread.GetNamedDataSlot()|ExternalThreading, SharedState|  
|System.Threading.Thread.Join()|ExternalThreading, Synchronization|  
|System.Threading.Thread.set_ApartmentState()|Synchronization, SelfAffectingThreading|  
|System.Threading.Thread.set_CurrentUICulture()|ExternalThreading|  
|System.Threading.Thread.set_IsBackground()|SelfAffectingThreading|  
|System.Threading.Thread.set_Name()|ExternalThreading|  
|System.Threading.Thread.set_Priority()|SelfAffectingThreading|  
|System.Threading.Thread.SetApartmentState()|Synchronization, SelfAffectingThreading|  
|System.Threading.Thread.SetData()|ExternalThreading, SharedState|  
|System.Threading.Thread.SpinWait()|ExternalThreading, Synchronization|  
|System.Threading.Thread.Start()|ExternalThreading, Synchronization|  
|System.Threading.Thread.TrySetApartmentState()|Synchronization, SelfAffectingThreading|  
|System.Threading.ThreadPool|ExternalThreading, Synchronization|  
|System.Threading.Timer|ExternalThreading, Synchronization|  
|System.Threading.TimerBase|ExternalThreading, Synchronization|  
  
## <a name="see-also"></a>Consulte también  
 [Atributos de protección del host y programación de la integración CLR](host-protection-attributes-and-clr-integration-programming.md)   
 [Tipos y miembros no permitidos en Microsoft.VisualBasic.dll](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [Tipos y miembros no permitidos en System.dll](disallowed-types-and-members-in-system-dll.md)   
 [Tipos y miembros no permitidos en System.Data.dll](disallowed-types-and-members-in-system-data-dll.md)   
 [Tipos y miembros no permitidos en System.Core.dll](disallowed-types-and-members-in-system-core-dll.md)  
  
  

---
title: Suplantación y credenciales para las conexiones | Microsoft Docs
description: En SQL Server integración con CLR, es posible que desee suplantar al autor de la llamada en la autenticación de Windows mediante la propiedad SqlContext. WindowsIdentity.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- impersonation [CLR integration]
- security [CLR integration]
- database objects [CLR integration], connections
- connections [CLR integration]
- authentication [CLR integration]
- user impersonation [CLR integration]
- credentials [CLR integration]
- database objects [CLR integration], security
ms.assetid: 293dce7d-1db2-4657-992f-8c583d6e9ebb
author: rothja
ms.author: jroth
ms.openlocfilehash: a6487b61d9c21ee86acad28413fb8a0439731b33
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810850"
---
# <a name="impersonation-and-credentials-for-connections"></a>Suplantación y credenciales para conexiones
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  En la integración con Common Language Runtime (CLR) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el uso de la autenticación de Windows es complejo, pero es más seguro que usar la autenticación de SOL Server. Al usar la autenticación de Windows, tenga presente las consideraciones siguientes.  
  
 De forma predeterminada, un proceso de SQL Server que se conecta a Windows adquiere el contexto de seguridad de la cuenta de servicio de Windows para SQL Server. Pero es posible asignar una función CLR a una identidad del proxy, para que sus conexiones salientes tengan un contexto de seguridad diferente que el de la cuenta del servicio de Windows.  
  
 En algunos casos, puede que desee suplantar al autor de la llamada mediante la propiedad **SqlContext. WindowsIdentity** en lugar de ejecutar como la cuenta de servicio. La instancia **WindowsIdentity** representa la identidad del cliente que invocó el código de llamada y solo está disponible cuando el cliente usó la autenticación de Windows. Una vez obtenida la instancia **WindowsIdentity** , puede llamar a **Impersonate** para cambiar el token de seguridad del subproceso y, a continuación, abrir las conexiones ADO.net en nombre del cliente.  
  
 Después de llamar a SQLContext. WindowsIdentity. Impersonate, no puede tener acceso a los datos locales y no puede tener acceso a los datos del sistema. Para acceder a los datos de nuevo, debe llamar a WindowsImpersonationContext. Undo.  
  
 En el ejemplo siguiente se muestra cómo suplantar al autor de la llamada mediante la propiedad **SqlContext. WindowsIdentity** .  
  
 Visual C#  
  
```  
WindowsIdentity clientId = null;  
WindowsImpersonationContext impersonatedUser = null;  
  
clientId = SqlContext.WindowsIdentity;  
  
// This outer try block is used to protect from   
// exception filter attacks which would prevent  
// the inner finally block from executing and   
// resetting the impersonation.  
try  
{  
   try  
   {  
      impersonatedUser = clientId.Impersonate();  
      if (impersonatedUser != null)  
         return GetFileDetails(directoryPath);  
         else return null;  
   }  
   finally  
   {  
      if (impersonatedUser != null)  
         impersonatedUser.Undo();  
   }  
}  
catch  
{  
   throw;  
}  
```  
  
> [!NOTE]  
>  Para obtener información sobre los cambios de comportamiento en la suplantación, vea [cambios importantes en las características de motor de base de datos en SQL Server 2016](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md).  
  
 Además, si obtuvo la instancia de identidad en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows, no puede propagar esa instancia a otro equipo de forma predeterminada; la infraestructura de seguridad de Windows restringe esa acción de forma predeterminada. Sin embargo, hay un mecanismo denominado "delegación" que habilita la propagación de identidades de Windows a través de varios equipos de confianza. Puede obtener más información sobre la delegación en el artículo de TechNet "[transición del protocolo Kerberos y delegación restringida](/previous-versions/windows/it-pro/windows-server-2003/cc739587(v=ws.10))".  
  
## <a name="see-also"></a>Consulte también  
 [Objeto SqlContext](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  

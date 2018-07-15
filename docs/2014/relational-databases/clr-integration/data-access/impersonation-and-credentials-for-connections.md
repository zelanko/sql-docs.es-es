---
title: Suplantación y credenciales para conexiones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
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
caps.latest.revision: 31
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9af64be53b702dfded163a06562e4f6bdf7e5a61
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37350884"
---
# <a name="impersonation-and-credentials-for-connections"></a>Suplantación y credenciales para conexiones
  En la integración con Common Language Runtime (CLR) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el uso de la autenticación de Windows es complejo, pero es más seguro que usar la autenticación de SOL Server. Al usar la autenticación de Windows, tenga presente las consideraciones siguientes.  
  
 De forma predeterminada, un proceso de SQL Server que se conecta a Windows adquiere el contexto de seguridad de la cuenta de servicio de Windows para SQL Server. Pero es posible asignar una función CLR a una identidad del proxy, para que sus conexiones salientes tengan un contexto de seguridad diferente que el de la cuenta del servicio de Windows.  
  
 En algunos casos, puede que desee suplantar al autor de las llamadas mediante la propiedad `SqlContext.WindowsIdentity` en lugar de ejecutarse como una cuenta de servicio. La instancia de `WindowsIdentity` representa la identidad del cliente que invocó el código de llamada y solo está disponible cuando el cliente usó la autenticación de Windows. Después de haber obtenido la instancia de `WindowsIdentity`, puede llamar a `Impersonate` para cambiar el token de seguridad del subproceso y, a continuación, abrir las conexiones de ADO.NET en nombre del cliente.  
  
 Después de llamar a SQLContext.WindowsIdentity.Impersonate, no se puede obtener acceso a datos locales y no se puede obtener acceso a los datos del sistema. Para obtener acceso a datos de nuevo, se debe llamar a WindowsImpersonationContext.Undo.  
  
 En el ejemplo siguiente se muestra cómo suplantar al autor de las llamadas mediante la propiedad `SqlContext.WindowsIdentity`.  
  
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
>  Para obtener información acerca de los cambios de comportamiento en la suplantación, vea [cambios recientes en las características del motor de base de datos de SQL Server 2014](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md).  
  
 Además, si obtuvo la instancia de identidad en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows, no puede propagar esa instancia a otro equipo de forma predeterminada; la infraestructura de seguridad de Windows restringe esa acción de forma predeterminada. Sin embargo, hay un mecanismo denominado "delegación" que habilita la propagación de identidades de Windows a través de varios equipos de confianza. Puede aprender más acerca de la delegación en el artículo de TechNet "[Kerberos Protocol Transition and Constrained Delegation](http://go.microsoft.com/fwlink/?LinkId=50419)".  
  
## <a name="see-also"></a>Vea también  
 [Objeto SqlContext](../../clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  
  

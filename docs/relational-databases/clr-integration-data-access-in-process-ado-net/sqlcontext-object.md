---
title: Objeto SqlContext | Microsoft Docs
description: Al invocar código administrado en SQL Server en una conexión de usuario, el acceso al contexto del llamador se abstrae en un objeto SqlContext.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- Windows identity [CLR integration]
- SqlContext object
- context [CLR integration]
ms.assetid: 67437853-8a55-44d9-9337-90689ebba730
author: rothja
ms.author: jroth
ms.openlocfilehash: cc3dc5787693345c531e7afb3384bf093dc17aa6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765445"
---
# <a name="sqlcontext-object"></a>Objeto SqlContext
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Se invoca el código administrado en el servidor al llamar a un procedimiento o función, al llamar a un método en un tipo definido por el usuario de Common Language Runtime (CLR) o cuando su acción activa un desencadenador definido en cualquiera de los lenguajes de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework. Dado que la ejecución de este código se solicita como parte de una conexión de usuario, se requiere el acceso al contexto del autor de la llamada desde el código que se ejecuta en el servidor. Además, ciertas operaciones de acceso a datos solo pueden ser válidas si se ejecutan bajo el contexto del autor de la llamada. Por ejemplo, el acceso a pseudo tablas insertadas y eliminadas utilizadas en operaciones del desencadenador solo es válido bajo el contexto del autor de la llamada.  
  
 El contexto del llamador se abstrae en un objeto **SqlContext** . Para obtener más información sobre los métodos y las propiedades de **SqlTriggerContext** , consulte la documentación de referencia de la clase **Microsoft. SqlServer. Server. SqlTriggerContext** en el [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
 **SqlContext** proporciona acceso a los siguientes componentes:  
  
-   **SqlPipe**: el objeto **SqlPipe** representa la "canalización" a través de la que los resultados fluyen al cliente. Para obtener más información sobre el objeto **SqlPipe** , vea [SqlPipe (objeto](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)).  
  
-   **SqlTriggerContext**: el objeto **SqlTriggerContext** solo se puede recuperar desde dentro de un desencadenador CLR. Proporciona información sobre la operación que hizo que se activara el desencadenador y un mapa de las columnas actualizadas. Para obtener más información sobre el objeto **SqlTriggerContext** , vea [objeto SqlTriggerContext](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md).  
  
-   **Isavailable**: la propiedad **isavailable** se usa para determinar la disponibilidad del contexto.  
  
-   **WindowsIdentity**: la propiedad **WindowsIdentity** se usa para recuperar la identidad de Windows del autor de la llamada.  
  
## <a name="determining-context-availability"></a>Determinar la disponibilidad del contexto  
 Consulte la clase **SqlContext** para ver si el código actualmente en ejecución se ejecuta en proceso. Para ello, Compruebe la propiedad **isavailable** del objeto **SqlContext** . La propiedad **isavailable** es de solo lectura y devuelve **true** si el código de llamada se ejecuta dentro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de y si se puede tener acceso a otros miembros de **SqlContext** . Si la propiedad **isavailable** devuelve **false**, todos los demás miembros de **SqlContext** producen una **excepción InvalidOperationException**, si se usa. Si **isavailable** devuelve **false**, se produce un error en cualquier intento de abrir un objeto de conexión que tenga "context Connection = true" en la cadena de conexión.  
  
## <a name="retrieving-windows-identity"></a>Recuperar la identidad de Windows  
 El código CLR que se ejecuta dentro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siempre se invoca en el contexto de la cuenta de proceso. Si el código debe realizar ciertas acciones mediante la identidad del usuario que realiza la llamada, en lugar de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identidad del proceso, se debe obtener un token de suplantación a través de la propiedad **WindowsIdentity** del objeto **SqlContext** . La propiedad **WindowsIdentity** devuelve una instancia de **WindowsIdentity** que representa la [!INCLUDE[msCoName](../../includes/msconame-md.md)] identidad de Windows del autor de la llamada, o null si el cliente se autenticó utilizando la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación de. Solo los ensamblados marcados con permisos de **external_access** o **no seguros** pueden tener acceso a esta propiedad.  
  
 Después de obtener el objeto **WindowsIdentity** , los autores de llamadas pueden suplantar la cuenta de cliente y realizar acciones en su nombre.  
  
 La identidad del autor de la llamada solo está disponible a través de **SqlContext. WindowsIdentity** si el cliente que inició la ejecución del procedimiento almacenado o la función está conectado al servidor mediante la autenticación de Windows. Si en su lugar se utilizara la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta propiedad sería NULL y el código no podría suplantar al autor de la llamada.  
  
### <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, se muestra cómo obtener la identidad de Windows del cliente de la llamada y suplantarla.  
  
 C#  
  
```  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void WindowsIDTestProc()  
{  
    WindowsIdentity clientId = null;  
    WindowsImpersonationContext impersonatedUser = null;  
  
    // Get the client ID.  
    clientId = SqlContext.WindowsIdentity;  
  
    // This outer try block is used to thwart exception filter   
    // attacks which would prevent the inner finally   
    // block from executing and resetting the impersonation.  
    try  
    {  
        try  
        {  
            impersonatedUser = clientId.Impersonate();  
            if (impersonatedUser != null)  
            {  
                // Perform some action using impersonation.  
            }  
        }  
        finally  
        {  
            // Undo impersonation.  
            if (impersonatedUser != null)  
                impersonatedUser.Undo();  
        }  
    }  
    catch  
    {  
        throw;  
    }  
}  
```  
  
 Visual Basic  
  
```  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub  WindowsIDTestProcVB ()  
    Dim clientId As WindowsIdentity  
    Dim impersonatedUser As WindowsImpersonationContext  
  
    ' Get the client ID.  
    clientId = SqlContext.WindowsIdentity  
  
    ' This outer try block is used to thwart exception filter   
    ' attacks which would prevent the inner finally   
    ' block from executing and resetting the impersonation.  
  
    Try  
        Try  
  
            impersonatedUser = clientId.Impersonate()  
  
            If impersonatedUser IsNot Nothing Then  
                ' Perform some action using impersonation.  
            End If  
  
        Finally  
            ' Undo impersonation.  
            If impersonatedUser IsNot Nothing Then  
                impersonatedUser.Undo()  
            End If  
        End Try  
  
    Catch e As Exception  
  
        Throw e  
  
    End Try  
End Sub  
```  
  
## <a name="see-also"></a>Consulte también  
 [SqlPipe (objeto)](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)   
 [Objeto SqlTriggerContext](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)   
 [Desencadenadores CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [Extensiones específicas en proceso de SQL Server a ADO.NET](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  

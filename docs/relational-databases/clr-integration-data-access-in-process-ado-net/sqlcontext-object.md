---
title: Objeto SqlContext | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- Windows identity [CLR integration]
- SqlContext object
- context [CLR integration]
ms.assetid: 67437853-8a55-44d9-9337-90689ebba730
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 627620311feafae43e41c23b65552c3f1d2f612c
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="sqlcontext-object"></a>Objeto SqlContext
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Se invoca el código administrado en el servidor al llamar a un procedimiento o función, al llamar a un método en un tipo definido por el usuario de Common Language Runtime (CLR) o cuando su acción activa un desencadenador definido en cualquiera de los lenguajes de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework. Dado que la ejecución de este código se solicita como parte de una conexión de usuario, se requiere el acceso al contexto del autor de la llamada desde el código que se ejecuta en el servidor. Además, ciertas operaciones de acceso a datos solo pueden ser válidas si se ejecutan bajo el contexto del autor de la llamada. Por ejemplo, el acceso a pseudo tablas insertadas y eliminadas utilizadas en operaciones del desencadenador solo es válido bajo el contexto del autor de la llamada.  
  
 El contexto del autor de la llamada se resume en un **SqlContext** objeto. Para obtener más información sobre la **SqlTriggerContext** métodos y propiedades, vea la **Microsoft.SqlServer.Server.SqlTriggerContext** documentación de referencia de la clase la [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
 **SqlContext** proporciona acceso a los siguientes componentes:  
  
-   **SqlPipe**: el **SqlPipe** objeto representa la "canalización" a través de que los resultados fluyen al cliente. Para obtener más información sobre la **SqlPipe** de objetos, consulte [SqlPipe, objetos](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md).  
  
-   **SqlTriggerContext**: el **SqlTriggerContext** objeto solo se pueden recuperar desde dentro de un desencadenador CLR. Proporciona información sobre la operación que hizo que se activara el desencadenador y un mapa de las columnas actualizadas. Para obtener más información sobre la **SqlTriggerContext** de objetos, consulte [SqlTriggerContext, objeto](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md).  
  
-   **IsAvailable**: el **IsAvailable** propiedad se utiliza para determinar la disponibilidad de contexto.  
  
-   **WindowsIdentity**: el **WindowsIdentity** propiedad se utiliza para recuperar la identidad de Windows del autor de la llamada.  
  
## <a name="determining-context-availability"></a>Determinar la disponibilidad del contexto  
 Consulta el **SqlContext** clase para ver si el código está ejecutando actualmente se ejecuta en proceso. Para ello, compruebe el **IsAvailable** propiedad de la **SqlContext** objeto. El **IsAvailable** propiedad es de solo lectura y devuelve **True** si el código de llamada se ejecuta dentro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y si otros **SqlContext** pueden tener acceso a los miembros. Si el **IsAvailable** propiedad devuelve **False**, todos los demás **SqlContext** los miembros de producir una **InvalidOperationException**, si se usa . Si **IsAvailable** devuelve **False**, cualquier intento de abrir un objeto de conexión que tiene "conexión de contexto = true" en la cadena de conexión se produce un error.  
  
## <a name="retrieving-windows-identity"></a>Recuperar la identidad de Windows  
 El código CLR que se ejecuta dentro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siempre se invoca en el contexto de la cuenta de proceso. Si el código debe realizar determinadas acciones utilizando la identidad del usuario que realiza la llamada, en lugar de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identidad, del proceso, a continuación, se debe obtener un token de suplantación a través de la **WindowsIdentity** propiedad de la  **SqlContext** objeto. El **WindowsIdentity** propiedad devuelve un **WindowsIdentity** instancia que representa el [!INCLUDE[msCoName](../../includes/msconame-md.md)] identidad de Windows de la llamada, o null si el cliente se autentica utilizando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Autenticación. Solo los ensamblados marcados con **EXTERNAL_ACCESS** o **UNSAFE** permisos pueden tener acceso a esta propiedad.  
  
 Después de obtener la **WindowsIdentity** de objeto, los llamadores pueden suplantar la cuenta del cliente y realizar acciones en su nombre.  
  
 Solo está disponible a través de la identidad del llamador **SqlContext.WindowsIdentity** si el cliente que inició la ejecución del procedimiento almacenado o la función conectado al servidor mediante la autenticación de Windows. Si en su lugar se utilizara la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta propiedad sería NULL y el código no podría suplantar al autor de la llamada.  
  
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
  
## <a name="see-also"></a>Vea también  
 [SqlPipe, objetos](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)   
 [Objeto SqlTriggerContext](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)   
 [Desencadenadores CLR](http://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [Extensiones específicas en proceso de SQL Server a ADO.NET](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  

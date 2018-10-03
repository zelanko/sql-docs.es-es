---
title: Objeto SqlContext | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: c14003652db37ca23addd2ac0dfd14ca0ada9f00
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47825293"
---
# <a name="sqlcontext-object"></a>Objeto SqlContext
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Se invoca el código administrado en el servidor al llamar a un procedimiento o función, al llamar a un método en un tipo definido por el usuario de Common Language Runtime (CLR) o cuando su acción activa un desencadenador definido en cualquiera de los lenguajes de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework. Dado que la ejecución de este código se solicita como parte de una conexión de usuario, se requiere el acceso al contexto del autor de la llamada desde el código que se ejecuta en el servidor. Además, ciertas operaciones de acceso a datos solo pueden ser válidas si se ejecutan bajo el contexto del autor de la llamada. Por ejemplo, el acceso a pseudo tablas insertadas y eliminadas utilizadas en operaciones del desencadenador solo es válido bajo el contexto del autor de la llamada.  
  
 El contexto de la persona que llama se abstrae en un **SqlContext** objeto. Para obtener más información sobre la **SqlTriggerContext** métodos y propiedades, vea el **Microsoft.SqlServer.Server.SqlTriggerContext** documentación de referencia en la clase el [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
 **SqlContext** proporciona acceso a los siguientes componentes:  
  
-   **SqlPipe**: el **SqlPipe** objeto representa la "canalización" por qué los resultados fluyen hacia el cliente. Para obtener más información sobre la **SqlPipe** de objetos, consulte [SqlPipe, objetos](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md).  
  
-   **SqlTriggerContext**: el **SqlTriggerContext** objeto sólo se puede recuperar desde dentro de un desencadenador CLR. Proporciona información sobre la operación que hizo que se activara el desencadenador y un mapa de las columnas actualizadas. Para obtener más información sobre la **SqlTriggerContext** de objetos, consulte [objeto SqlTriggerContext](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md).  
  
-   **IsAvailable**: el **IsAvailable** propiedad se utiliza para determinar la disponibilidad de contexto.  
  
-   **WindowsIdentity**: el **WindowsIdentity** propiedad se utiliza para recuperar la identidad de Windows del llamador.  
  
## <a name="determining-context-availability"></a>Determinar la disponibilidad del contexto  
 Consulta el **SqlContext** clase para ver si el código que se está ejecutando actualmente se está ejecutando en proceso. Para ello, compruebe el **IsAvailable** propiedad de la **SqlContext** objeto. El **IsAvailable** propiedad es de solo lectura y devuelve **True** si se está ejecutando el código de llamada dentro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y si otros **SqlContext** pueden tener acceso a miembros. Si el **IsAvailable** propiedad devuelve **False**, todos los demás **SqlContext** los miembros de producir una **InvalidOperationException**, si se usa . Si **IsAvailable** devuelve **False**, cualquier intento de abrir un objeto de conexión que tiene "conexión de contexto = true" en la cadena de conexión se produce un error.  
  
## <a name="retrieving-windows-identity"></a>Recuperar la identidad de Windows  
 El código CLR que se ejecuta dentro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siempre se invoca en el contexto de la cuenta de proceso. Si el código debe realizar algunas acciones utilizando la identidad del usuario que realiza la llamada, en lugar de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identidad de proceso, a continuación, se debe obtener un token de suplantación a través de la **WindowsIdentity** propiedad de la  **SqlContext** objeto. El **WindowsIdentity** propiedad devuelve un **WindowsIdentity** instancia que representa el [!INCLUDE[msCoName](../../includes/msconame-md.md)] identidad de Windows del llamador, o null si el cliente se autenticó utilizando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Autenticación. Solo los ensamblados marcados con **EXTERNAL_ACCESS** o **UNSAFE** permisos pueden tener acceso a esta propiedad.  
  
 Después de obtener el **WindowsIdentity** de objeto, los autores de llamadas pueden suplantar la cuenta de cliente y realizar acciones en su nombre.  
  
 Solo está disponible a través de la identidad del llamador **SqlContext.WindowsIdentity** si el cliente que inició la ejecución del procedimiento almacenado o función conectado al servidor mediante la autenticación de Windows. Si en su lugar se utilizara la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta propiedad sería NULL y el código no podría suplantar al autor de la llamada.  
  
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
 [Objeto SqlPipe](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)   
 [Objeto SqlTriggerContext](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)   
 [Desencadenadores CLR](http://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [Extensiones específicas en proceso de SQL Server a ADO.NET](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  

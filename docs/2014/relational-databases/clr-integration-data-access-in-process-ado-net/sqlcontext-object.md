---
title: Objeto SqlContext | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 223111874ca34ba4df4968c550e6cc47edf2b390
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48062953"
---
# <a name="sqlcontext-object"></a>Objeto SqlContext
  Se invoca el código administrado en el servidor al llamar a un procedimiento o función, al llamar a un método en un tipo definido por el usuario de Common Language Runtime (CLR) o cuando su acción activa un desencadenador definido en cualquiera de los lenguajes de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework. Dado que la ejecución de este código se solicita como parte de una conexión de usuario, se requiere el acceso al contexto del autor de la llamada desde el código que se ejecuta en el servidor. Además, ciertas operaciones de acceso a datos solo pueden ser válidas si se ejecutan bajo el contexto del autor de la llamada. Por ejemplo, el acceso a pseudo tablas insertadas y eliminadas utilizadas en operaciones del desencadenador solo es válido bajo el contexto del autor de la llamada.  
  
 El contexto del autor de la llamada se resume en un objeto `SqlContext`. Para obtener más información sobre los métodos y propiedades de `SqlTriggerContext`, vea la documentación de referencia de clase `Microsoft.SqlServer.Server.SqlTriggerContext` en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
 `SqlContext` proporciona acceso a los componentes siguientes:  
  
-   `SqlPipe`: el objeto `SqlPipe` representa la "canalización" a través de la que los resultados fluyen al cliente. Para obtener más información sobre la `SqlPipe` de objetos, consulte [SqlPipe, objetos](sqlpipe-object.md).  
  
-   `SqlTriggerContext`: el objeto `SqlTriggerContext` solo se puede recuperar desde un desencadenador CLR. Proporciona información sobre la operación que hizo que se activara el desencadenador y un mapa de las columnas actualizadas. Para obtener más información sobre la `SqlTriggerContext` de objetos, consulte [objeto SqlTriggerContext](sqltriggercontext-object.md).  
  
-   `IsAvailable`: la propiedad `IsAvailable` se utiliza para determinar la disponibilidad de contexto.  
  
-   `WindowsIdentity`: la propiedad `WindowsIdentity` se utiliza para recuperar la identidad de Windows del autor de la llamada.  
  
## <a name="determining-context-availability"></a>Determinar la disponibilidad del contexto  
 Consulte la clase `SqlContext` para ver si el código actualmente en ejecución se ejecuta en proceso. Para ello, compruebe la propiedad `IsAvailable` del objeto `SqlContext`. La propiedad `IsAvailable` es de solo lectura y devuelve `True` si el código de llamada se está ejecutando dentro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y si se puede tener acceso a otros miembros de `SqlContext`. Si la propiedad `IsAvailable` devuelve `False`, todos los demás miembros de `SqlContext` producen una excepción `InvalidOperationException`, si se utilizan. Si `IsAvailable` devuelve `False`, cualquier intento de abrir un objeto de conexión con "context connection=true" en la cadena de conexión genera un error.  
  
## <a name="retrieving-windows-identity"></a>Recuperar la identidad de Windows  
 El código CLR que se ejecuta dentro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siempre se invoca en el contexto de la cuenta de proceso. Si el código debe realizar determinadas acciones utilizando la identidad del usuario que es el autor de la llamada, en lugar de la identidad del proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se debe obtener un token de suplantación a través de la propiedad `WindowsIdentity` del objeto `SqlContext`. La propiedad `WindowsIdentity` devuelve una instancia de `WindowsIdentity` que representa la identidad en Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)] del autor de la llamada, o bien, null si el cliente se autenticó utilizando la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Solo los ensamblados marcados con los permisos `EXTERNAL_ACCESS` o `UNSAFE` tienen acceso a esta propiedad.  
  
 Después de obtener el objeto `WindowsIdentity`, los autores de la llamada pueden suplantar la cuenta del cliente y realizar acciones en su nombre.  
  
 La identidad del autor de la llamada solo está disponible a través de `SqlContext.WindowsIdentity` si el cliente que inició la ejecución del procedimiento almacenado o función se conectó al servidor utilizando la autenticación de Windows. Si en su lugar se utilizara la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta propiedad sería NULL y el código no podría suplantar al autor de la llamada.  
  
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
 [Objeto SqlPipe](sqlpipe-object.md)   
 [Objeto SqlTriggerContext](sqltriggercontext-object.md)   
 [Desencadenadores CLR](../../database-engine/dev-guide/clr-triggers.md)   
 [Extensiones específicas en proceso de SQL Server a ADO.NET](sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  

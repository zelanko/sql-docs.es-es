---
title: Depurar objetos de base de datos CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- database objects [CLR integration], debugging
- permissions [CLR integration]
- debugging [CLR integration]
- building database objects [CLR integration], debugging
- common language runtime [SQL Server], debugging
ms.assetid: 1332035c-d6ed-424d-8234-46ad21168319
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f6811dc26bf473d5b720f843735f5f2f2ef3bab0
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51670634"
---
# <a name="debugging-clr-database-objects"></a>Depurar objetos de bases de datos CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona compatibilidad con la depuración de objetos de [!INCLUDE[tsql](../../includes/tsql-md.md)] y Common Language Runtime (CLR) en la base de datos. Los aspectos clave de la depuración en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son la facilidad de configuración y uso, y la integración del depurador de SQL Server con el depurador de Microsoft Visual Studio. Además, la depuración se produce en todos los lenguajes. Los usuarios pueden pasar sin problemas a objetos de CLR desde [!INCLUDE[tsql](../../includes/tsql-md.md)] y viceversa. El depurador de Transact-SQL en SQL Server Management Studio no se puede utilizar para depurar objetos de base de datos administrados, pero se pueden depurar los objetos utilizando los depuradores de Visual Studio. La depuración de objetos de base de datos administrados en Visual Studio admite todas las funciones habituales de depuración, como las instrucciones "ir a" y "paso a paso por procedimientos" dentro de rutinas que se ejecutan en el servidor. Los depuradores pueden establecer puntos de interrupción, inspeccionar la pila de llamadas, inspeccionar variables y modificar valores de variables durante la depuración. Tenga en cuenta que Visual Studio .NET 2003 no puede utilizarse para programar o depurar la integración CLR. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye .NET Framework preinstalado y Visual Studio .NET 2003 no puede utilizar los ensamblados de .NET Framework 2.0.  
  
 Para obtener más información sobre cómo depurar código administrado con Visual Studio, consulte el "[Debugging Managed Code](https://go.microsoft.com/fwlink/?LinkId=120377)" tema en la documentación de Visual Studio.  
  
## <a name="debugging-permissions-and-restrictions"></a>Permisos y restricciones de depuración  
 La depuración es una operación con privilegios elevados y, por tanto, solo los miembros de la **sysadmin** fijo de servidor tienen permiso para ello, en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Las restricciones siguientes se aplican durante la depuración:  
  
-   La depuración de rutinas CLR está restringida a una instancia del depurador cada vez. Esta limitación se aplica porque toda la ejecución de código de CLR se inmoviliza cuando se alcanza un punto de interrupción y la ejecución no continúa hasta que el depurador pasa el punto de interrupción. Sin embargo, se puede seguir depurando [!INCLUDE[tsql](../../includes/tsql-md.md)] en otras conexiones. Aunque la depuración de [!INCLUDE[tsql](../../includes/tsql-md.md)] no inmoviliza otras ejecuciones en el servidor, puede hacer que otras conexiones tengan que esperar por el mantenimiento de un bloqueo.  
  
-   Las conexiones existentes no se pueden depurar; solo se pueden depurar las conexiones nuevas, ya que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere información sobre el cliente y el entorno del depurador antes de que se pueda realizar la conexión.  
  
 Debido a las restricciones anteriores, se recomienda que el código [!INCLUDE[tsql](../../includes/tsql-md.md)] y CLR se depure en un servidor de prueba y no en un servidor de producción.  
  
## <a name="overview-of-debugging-managed-database-objects"></a>Información general de la depuración de objetos de base de datos administrados  
 La depuración en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sigue un modelo por conexión. Un depurador solo puede detectar y depurar actividades en la conexión de cliente a la que está adjuntado. Dado que la funcionalidad del depurador no está limitada por el tipo de conexión, se pueden depurar flujos TDS y conexiones HTTP. Sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite la depuración de conexiones existentes. La depuración admite todas las características habituales de depuración dentro de rutinas que se ejecutan en el servidor. La interacción entre un depurador y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se produce mediante un modelo de objetos componentes (COM) distribuido.  
  
 Para obtener más información y situaciones sobre cómo depurar procedimientos almacenados administrados, funciones, desencadenadores, tipos definidos por el usuario y agregados, vea el "[depuración de la base de datos de integración CLR de SQL Server](https://go.microsoft.com/fwlink/?LinkId=120378)" tema en Visual Studio documentación.  
  
 El protocolo de red TCP/IP debe estar habilitado en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a fin de utilizar Visual Studio para el desarrollo remoto, la depuración y el desarrollo. Para obtener más información acerca de cómo habilitar el protocolo TCP/IP en el servidor, consulte [configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md).  
  
#### <a name="to-debug-a-managed-database-object"></a>Para depurar un objeto de base de datos administrado  
  
1.  Abra Microsoft Visual Studio, cree un nuevo proyecto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y establezca una conexión a una base de datos en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Cree un nuevo tipo. En **el Explorador de soluciones**, haga clic en el proyecto, seleccione **agregar** y **nuevo elemento...** Desde el **Agregar nuevo elemento** ventana, seleccione **Stored Procedure**, **función definida por el usuario**, **User-Defined Type**,  **Desencadenador**, **agregado**, o **clase**. Especifique un nombre para el archivo de origen del nuevo tipo y haga clic en **agregar**.  
  
3.  Agregue código para el nuevo tipo al editor de texto. En la sección que figura más adelante en este tema, puede ver el código de ejemplo de un procedimiento almacenado de ejemplo.  
  
4.  Agregue un script que pruebe el tipo. En **el Explorador de soluciones**, expanda el **TestScripts** directory haga doble clic en **Test.sql** para abrir el archivo de origen del script de prueba predeterminado. Agregue al editor de texto el script de prueba, uno que llame al código que se va a depurar. Vea más adelante un script de ejemplo.  
  
5.  Coloque uno o más puntos de interrupción en el código fuente. Haga doble clic en una línea de código en el editor de texto dentro de la función o rutina que desea depurar, y seleccione **punto de interrupción** y **Insertar punto de interrupción**. Se agrega el punto de interrupción, resaltando la línea de código en rojo.  
  
6.  En el **depurar** menú, seleccione **Iniciar depuración** para compilar, implementar y probar el proyecto. Se ejecutará el script de prueba de Test.sql y se llamará al objeto de base de datos administrado.  
  
7.  Cuando la flecha amarilla que designa el puntero de instrucción aparece en el punto de interrupción, la ejecución del código se detiene y se puede empezar a depurar el objeto de base de datos administrado. También puede **saltar** desde el **depurar** menú para avanzar el puntero de instrucción a la siguiente línea de código. El **variables locales** ventana se utiliza para observar el estado de los objetos actualmente resaltado por el puntero de instrucción. Las variables se pueden agregar a la **inspección** ventana. El estado de las variables inspeccionadas se puede observar en toda la sesión de depuración, no solo cuando la variable está en la línea de código resaltada actualmente por el puntero de instrucción. Seleccione Continuar en el menú Depurar para hacer avanzar el puntero de instrucción hasta el siguiente punto de interrupción o para completar la ejecución de la rutina si no hay más puntos de interrupción.  
  
### <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se devuelve la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al autor de la llamada.  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void GetVersion()  
   {  
   using(SqlConnection connection = new SqlConnection("context connection=true"))   
   {  
      connection.Open();  
      SqlCommand command = new SqlCommand("select @@version",  
                                           connection);  
      SqlContext.Pipe.ExecuteAndSend(command);  
      }  
   }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
Partial Public Class StoredProcedures   
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub GetVersion()  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT @@VERSION", connection)  
            SqlContext.Pipe.ExecuteAndSend(command)  
        End Using  
    End Sub  
End Class  
```  
  
 A continuación se muestra un script de prueba que llama al procedimiento almacenado GetVersion definido anteriormente.  
  
```  
EXEC GetVersion  
```  
  
## <a name="see-also"></a>Vea también  
 [Conceptos de programación en el ámbito de la integración de Common Language Runtime &#40;CLR&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  

---
title: Depurar objetos de base de datos de Common Language Runtime (CLR)
description: SQL Server proporciona compatibilidad para depurar objetos de Transact-SQL y CLR en la base de datos que integra SQL Server Debugger con Microsoft Visual Studio Debugger.
ms.date: 10/06/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: how-to
helpviewer_keywords:
- database objects [CLR integration], debugging
- permissions [CLR integration]
- debugging [CLR integration]
- building database objects [CLR integration], debugging
- common language runtime [SQL Server], debugging
ms.assetid: 1332035c-d6ed-424d-8234-46ad21168319
author: rothja
ms.author: jroth
ms.openlocfilehash: 2a6e723c8ad5ff8c97a3b57edb554092211da4d7
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2020
ms.locfileid: "91785167"
---
# <a name="how-to-debug-clr-database-objects"></a>Cómo depurar objetos de base de datos CLR

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
 
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona compatibilidad con la depuración de objetos de [!INCLUDE[tsql](../../includes/tsql-md.md)] y Common Language Runtime (CLR) en la base de datos. Los aspectos clave de la depuración en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son la facilidad de configuración y uso, y la integración del depurador de SQL Server con el depurador de Microsoft Visual Studio. Además, la depuración se produce en todos los lenguajes. Los usuarios pueden pasar sin problemas a objetos de CLR desde [!INCLUDE[tsql](../../includes/tsql-md.md)] y viceversa. El depurador de Transact-SQL en SQL Server Management Studio no se puede utilizar para depurar objetos de base de datos administrados, pero se pueden depurar los objetos utilizando los depuradores de Visual Studio. La depuración de objetos de base de datos administrados en Visual Studio admite todas las funciones habituales de depuración, como las instrucciones "ir a" y "paso a paso por procedimientos" dentro de rutinas que se ejecutan en el servidor. Los depuradores pueden establecer puntos de interrupción, inspeccionar la pila de llamadas, inspeccionar variables y modificar valores de variables durante la depuración. 

> [!NOTE]
> Visual Studio .NET 2003 no se puede usar para la programación o depuración de la integración CLR. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye .NET Framework preinstalado y Visual Studio .NET 2003 no puede utilizar los ensamblados de .NET Framework 2.0.  
  
## <a name="debugging-permissions-and-restrictions"></a>Restricciones y permisos de depuración

La depuración es una operación con privilegios elevados y, por lo tanto, solo los miembros del rol fijo de servidor **sysadmin** pueden hacerlo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Las restricciones siguientes se aplican durante la depuración:  
  
- La depuración de rutinas CLR está restringida a una instancia del depurador cada vez. Esta limitación se aplica porque toda la ejecución de código de CLR se inmoviliza cuando se alcanza un punto de interrupción y la ejecución no continúa hasta que el depurador pasa el punto de interrupción. Sin embargo, se puede seguir depurando [!INCLUDE[tsql](../../includes/tsql-md.md)] en otras conexiones. Aunque la depuración de [!INCLUDE[tsql](../../includes/tsql-md.md)] no inmoviliza otras ejecuciones en el servidor, puede hacer que otras conexiones tengan que esperar por el mantenimiento de un bloqueo.  
  
- Las conexiones existentes no se pueden depurar; solo se pueden depurar las conexiones nuevas, ya que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere información sobre el cliente y el entorno del depurador antes de que se pueda realizar la conexión.  
  
Debido a las restricciones anteriores, se recomienda que el código [!INCLUDE[tsql](../../includes/tsql-md.md)] y CLR se depure en un servidor de prueba y no en un servidor de producción.  
  
## <a name="overview"></a>Introducción

La depuración en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sigue un modelo por conexión. Un depurador solo puede detectar y depurar actividades en la conexión de cliente a la que está adjuntado. Dado que la funcionalidad del depurador no está limitada por el tipo de conexión, se pueden depurar flujos TDS y conexiones HTTP. Sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite la depuración de conexiones existentes. La depuración admite todas las características habituales de depuración dentro de rutinas que se ejecutan en el servidor. La interacción entre un depurador y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se produce mediante un modelo de objetos componentes (COM) distribuido.  
  
Para obtener más información y escenarios sobre la depuración de procedimientos almacenados, funciones, desencadenadores, tipos definidos por el usuario y agregados administrados, vea [SQL Server depuración de base de datos de integración CLR](https://go.microsoft.com/fwlink/?LinkId=120378) en la documentación de Visual Studio.  
  
El protocolo de red TCP/IP debe estar habilitado en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a fin de utilizar Visual Studio para el desarrollo remoto, la depuración y el desarrollo. Para obtener más información acerca de cómo habilitar el protocolo TCP/IP en el servidor, vea [configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md).  
  
## <a name="debugging-steps"></a>Pasos de depuración

Siga los pasos que se indican a continuación para depurar un objeto de base de datos CLR en Microsoft Visual Studio:

1. Abra Microsoft Visual Studio y cree un nuevo proyecto de SQL Server. Puede usar la instancia de SQL LocalDB que viene con Visual Studio.

2. Crear un nuevo tipo de CLR de SQL (C#):

   1. En **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y seleccione **Agregar**, **nuevo elemento.**... 
   1. En la ventana **Agregar nuevo elemento** , seleccione **procedimiento almacenado de c# de SQL**CLR, **función definida por el usuario de SQL CLR c#**, **tipo definido por el usuario de SQL CLR c#**, **desencadenador de c# de SQL**CLR, agregado de c# de **SQL CLR**o **clase**.
   1. Especifique un nombre para el archivo de origen del nuevo tipo y, a continuación, seleccione **Agregar**.

3. Agregue código para el nuevo tipo al editor de texto. Para ver el código de ejemplo de un procedimiento almacenado de ejemplo, consulte la sección ejemplo siguiente de este artículo.

4. Agregue un script que pruebe el tipo: 

   1. En **Explorador de soluciones**, haga clic con el botón derecho en el nodo del proyecto y seleccione **Agregar**, **script..**.. 
   1. En la ventana **Agregar nuevo elemento** , seleccione **script (no está en la compilación)** y especifique un nombre, como `Test.sql` . Seleccione el botón **Agregar**.
   1. En **Explorador de soluciones**, haga doble clic en el `Test.sql` nodo para abrir el archivo de origen del script de prueba predeterminado.
   1. Agregue el script de prueba (uno que invoca el código que se va a depurar) al editor de texto. Vea el ejemplo de la sección siguiente para obtener un script de ejemplo.

5. Coloque uno o más puntos de interrupción en el código fuente. Haga clic con el botón derecho en una línea de código en el editor de texto de la función o rutina que desea depurar. Seleccione **punto de interrupción**, **Insertar punto de interrupción**. Se agrega el punto de interrupción, resaltando la línea de código en rojo.

6. En el menú **depurar** , seleccione **iniciar depuración** para compilar, implementar y probar el proyecto. Se ejecuta el script de prueba en `Test.sql` y se invoca el objeto de base de datos administrado.

7. Cuando la flecha amarilla (que designa el puntero de instrucción) aparece en el punto de interrupción, se detiene la ejecución del código. Después, puede depurar el objeto de base de datos administrado:

   1. Utilice **paso a paso por procedimientos** en el menú **depurar** para avanzar el puntero de instrucción hasta la siguiente línea de código.
   1. Use la ventana **variables locales** para observar el estado de los objetos resaltados actualmente por el puntero de instrucción.
   1. Agregar variables a la ventana **inspección** . Puede observar el estado de las variables inspeccionadas a lo largo de la sesión de depuración, aunque la variable no esté en la línea de código resaltada actualmente por el puntero de instrucción. 
   1. Seleccione **continuar** en el menú **depurar** para avanzar el puntero de instrucción hasta el siguiente punto de interrupción o para completar la ejecución de la rutina si no hay más puntos de interrupción.
  
## <a name="example-code"></a>Ejemplo de código

En el ejemplo siguiente se devuelve la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al autor de la llamada.  
  
```csharp
using System.Data.SqlClient;
using Microsoft.SqlServer.Server;

public class StoredProcedures
{
    [Microsoft.SqlServer.Server.SqlProcedure]
    public static void GetVersion()
    {
        using (var connection = new SqlConnection("context connection=true"))
        {
            connection.Open();
            var command = new SqlCommand("select @@version", connection);
            SqlContext.Pipe.ExecuteAndSend(command);
        }
    }
}
```

## <a name="example-test-script"></a>Script de prueba de ejemplo

El siguiente script de prueba muestra cómo invocar el `GetVersion` procedimiento almacenado definido en el ejemplo anterior.  
  
```sql
EXEC GetVersion  
```  

## <a name="next-steps"></a>Pasos siguientes
  
Para obtener más información sobre cómo depurar código administrado con Visual Studio, vea [depurar código administrado](https://go.microsoft.com/fwlink/?LinkId=120377) en la documentación de Visual Studio.  

Para obtener más información, vea conceptos de programación de la [integración de Common Language Runtime](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  

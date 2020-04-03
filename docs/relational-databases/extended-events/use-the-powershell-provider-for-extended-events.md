---
title: Usar el proveedor de PowerShell para eventos extendidos
description: Use el proveedor SQL Server PowerShell para administrar eventos extendidos de SQL Server. En este artículo se muestran ejemplos de creación, modificación y administración de sesiones.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- PowerShell [SQL Server], xevent
- extended events [SQL Server], PowerShell
- PowerShell [SQL Server], extended events
ms.assetid: 0b10016f-a479-4444-a484-46cb4677cf64
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 86c1aeeca719fff8f63926ff1c28fb810f0c5d8f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "79487563"
---
# <a name="use-the-powershell-provider-for-extended-events"></a>Usar el proveedor de PowerShell para eventos extendidos

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Puede administrar los eventos extendidos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando el proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell. La subcarpeta XEvent está disponible en la unidad SQLSERVER. Para acceder a la carpeta, puede usar cualquiera de los métodos siguientes:  
  
-   En el símbolo del sistema, escriba **sqlps**y luego presione ENTRAR. Escriba **cd xevent**y, a continuación, presione ENTRAR. Desde allí, puede usar los comandos **cd** y **dir** (o los cmdlets **Set-Location** y **Get-Childitem** ) para desplazarse al nombre del servidor y el nombre de la instancia.  
  
-   En el Explorador de objetos, expanda el nombre de la instancia, expanda **Administración**, haga clic con el botón derecho en **Eventos extendidos**y haga clic en **Iniciar PowerShell**. De esta forma, se inicia PowerShell en la siguiente ruta de acceso:  
  
     PS SQLSERVER:\XEvent\\*nombreDeServidor*\\*nombreDeInstancia*>  
  
    > [!NOTE]  
    >  Puede iniciar PowerShell en cualquier nodo situado debajo de **Eventos extendidos**. Por ejemplo, puede hacer clic con el botón derecho en **Sesiones**y, después, hacer clic en **Iniciar PowerShell**. De esta forma, se inicia PowerShell en un nivel más profundo de la carpeta Sessions.  
  
 Puede examinar el árbol de carpetas XEvent para ver las sesiones de eventos extendidos, así como sus eventos, destinos y predicados asociados. Por ejemplo, desde la ruta de acceso PS SQLSERVER:\XEvent\\*nombreDeServidor*\\*nombreDeInstancia*>, si escribe **cd sessions**, pulsa ENTRAR, escribe **dir** y pulsa ENTRAR, puede ver la lista de las sesiones almacenadas en esa instancia. Asimismo, puede ver si la sesión se está ejecutando (y si este es el caso, durante cuánto tiempo), así como si la sesión está configurada para iniciarse cuando se inicie la instancia.  
  
 Para ver los eventos, sus predicados y los destinos asociados con una sesión, puede cambiar los directorios al nombre de la sesión y, a continuación, ver la carpeta de eventos o de destino. Por ejemplo, para ver los eventos y sus predicados que están asociados con la sesión de estado del sistema predeterminada, desde la ruta de acceso PS SQLSERVER:\XEvent\\*nombreDeServidor*\\*nombreDeInstancia*\Sessions>, escriba **cd system_health\events,** pulse ENTRAR, escriba **dir** y pulse ENTRAR.  
  
 El proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell es una herramienta eficaz que puede usar para crear, modificar y administrar sesiones de eventos extendidos. En la siguiente sección se proporcionan algunos ejemplos básicos del uso de los scripts de PowerShell con eventos extendidos.  
  
## <a name="examples"></a>Ejemplos  
 En los siguientes ejemplos, observe lo siguiente:  
  
-   Los scripts se deben ejecutar desde el símbolo del sistema PS SQLSERVER:\\> (disponible si se escribe **sqlps** en un símbolo del sistema).  
  
-   Los scripts usan la instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Los scripts se deben guardar con una extensión .ps1.  
  
-   La directiva de ejecución de PowerShell debe permitir que se ejecute el script. Para establecer la directiva de ejecución, use el cmdlet **Set-Executionpolicy** . (Para obtener más información, escriba **get-help set-executionpolicy -detailed**y pulse ENTRAR).  
  
 En el siguiente script se crea una nueva sesión denominada 'TestSession'.  
  
```  
#Script for creating a session.  
cd XEvent  
$h = hostname  
cd $h  
  
#Use the default instance.  
$store = dir | where {$_.DisplayName -ieq 'default'}  
$session = new-object Microsoft.SqlServer.Management.XEvent.Session -argumentlist $store, "TestSession"  
$event = $session.AddEvent("sqlserver.file_written")  
$event.AddAction("package0.callstack")  
$session.Create()  
```  
  
 En el siguiente script se agrega el destino de búfer de anillo a la sesión creada en el ejemplo anterior. (Este ejemplo muestra el uso del método **Alter** . Tenga en cuenta que puede agregar el destino cuando cree la sesión por primera vez).  
  
```  
#Script to alter a session.  
cd XEvent  
$h = hostname  
cd $h  
cd DEFAULT\Sessions  
  
#Used to find the specified session.  
$session = dir|where {$_.Name -eq 'TestSession'}  
  
#Add the ring buffer target and call the Alter method.  
$session.AddTarget("package0.ring_buffer")  
$session.Alter()  
```  
  
 En el siguiente script se crea una nueva sesión que usa una expresión de predicado. En este caso, la sesión recopila información para cuando se escriba el archivo c:\temp.log (mediante el evento sqlserver.file_written).  
  
```  
#Script for creating a session.  
cd XEvent  
$h = hostname  
cd $h  
  
#Use the default instance.  
$store = dir | where {$_.DisplayName -ieq 'default'}  
$session = new-object Microsoft.SqlServer.Management.XEvent.Session -argumentlist $store, "TestSession2"  
$event = $session.AddEvent("sqlserver.file_written")  
  
#Construct a predicate "equal_i_unicode_string(path, N'c:\temp.log')".  
$column = $store.SqlServerPackage.EventInfoSet["file_written"].DataEventColumnInfoSet["path"]  
$operand = new-object Microsoft.SqlServer.Management.XEvent.PredOperand -argumentlist $column  
$value = new-object Microsoft.SqlServer.Management.XEvent.PredValue -argumentlist "c:\temp.log"  
$compare = $store.Package0Package.PredCompareInfoSet["equal_i_unicode_string"]  
$predicate = new-object Microsoft.SqlServer.Management.XEvent.PredFunctionExpr -argumentlist $compare, $operand, $value  
$event.SetPredicate($predicate)  
$session.Create()  
```  
  
## <a name="security"></a>Seguridad  
 Para crear, modificar o quitar una sesión de eventos extendidos, debe disponer del permiso ALTER ANY EVENT SESSION.  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)   
 [Usar la sesión system_health](../../relational-databases/extended-events/use-the-system-health-session.md)   
 [Herramientas de eventos extendidos](../../relational-databases/extended-events/extended-events-tools.md)  
  
  

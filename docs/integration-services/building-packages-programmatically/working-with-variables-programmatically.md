---
title: "Trabajar con Variables mediante programación | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- System namespace
- scope [Integration Services]
- variables [Integration Services], programmatically
- configuration files [Integration Services]
- Variables collection
- User namespace
- custom variables [Integration Services]
- variables [Integration Services], customizing
ms.assetid: c4b76a3d-94ca-4a8e-bb45-cb8bd0ea3ec1
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 5c8968302f42e1b8fde55894810ecb77cf715ab6
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="working-with-variables-programmatically"></a>Trabajar con variables mediante programación
  Las variables son una manera de establecer valores y controlar procesos en paquetes, contenedores, tareas y controladores de eventos de forma dinámica. Las restricciones de precedencia también pueden usar variables para controlar la dirección del flujo de datos en diferentes tareas. Las variables tienen diversos usos:  
  
-   Actualizan las propiedades de un paquete en tiempo de ejecución.  
  
-   Rellenan los valores de parámetros para instrucciones Transact-SQL en tiempo de ejecución.  
  
-   Controlan el flujo de un bucle Foreach. Para obtener más información, consulte [agregar enumeración a un flujo de Control](http://msdn.microsoft.com/library/f212b5fb-3cc4-422e-9b7c-89eb769a812a).  
  
-   Controlan una restricción de precedencia por su uso en una expresión. Una restricción de precedencia puede incluir variables en la definición de restricción. Para obtener más información, vea [Agregar expresiones a las restricciones de precedencia](http://msdn.microsoft.com/library/5574d89a-a68e-4b84-80ea-da93305e5ca1).  
  
-   Controlan la repetición condicional de un contenedor de bucles For. Para obtener más información, consulte [agregar iteración a un flujo de Control](http://msdn.microsoft.com/library/eb3a7494-88ae-4165-9d0f-58715eb1734a).  
  
-   Generan expresiones que incluyen valores de variable.  
  
-   Puede crear variables personalizadas para todos los tipos de contenedor: paquetes, **bucles Foreach** contenedores, **de bucles for** contenedores, **secuencia** contenedores, TaskHosts y controladores de eventos. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) y [Usar variables en paquetes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="scope"></a>Ámbito  
 Cada contenedor tiene su propia colección <xref:Microsoft.SqlServer.Dts.Runtime.Variables>. Cuando se crea una nueva variable, está dentro del ámbito de su contenedor primario. Dado que el contenedor del paquete se encuentra en la parte superior de la jerarquía de contenedores, las variables con ámbito de paquete funcionan como variables globales y están visibles para todos los contenedores del paquete. Los elementos secundarios del contenedor también pueden tener acceso a la colección de variables para el contenedor a través de la colección <xref:Microsoft.SqlServer.Dts.Runtime.Variables>, utilizando el nombre de variable o el índice de la variable en la colección.  
  
 Dado que la visibilidad de una variable afecta desde arriba hacia abajo, las variables declaradas en el nivel de paquete están visibles para todos los contenedores del paquete. Por consiguiente, la colección <xref:Microsoft.SqlServer.Dts.Runtime.Variables> de un contenedor incluye todas las variables que pertenecen a su elemento primario además de sus propias variables.  
  
 Por el contrario, las variables contenidas en una tarea se limitan en ámbito y visibilidad, y únicamente están visible para la tarea.  
  
 Si un paquete ejecuta otros paquetes, las variables definidas en el ámbito del paquete que llama se ponen a disposición del paquete llamado. La única excepción se produce cuando existe una variable con el mismo nombre en el paquete llamado. Cuando se produce esta colisión, el valor de variable del paquete llamado invalida el valor del paquete que llama. Las variables definidas en el ámbito del paquete llamado nunca vuelven a ponerse a disposición del paquete que llama.  
  
 En el ejemplo de código siguiente se crea una variable, `myCustomVar`, mediante programación en el ámbito del paquete y, a continuación, se itera a través de todas las variables visibles al paquete, imprimiendo su nombre, tipo de datos y valor.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Application app = new Application();  
      // Load a sample package that contains a variable that sets the file name.  
      Package pkg = app.LoadPackage(  
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\CaptureDataLineage Sample\CaptureDataLineage\CaptureDataLineage.dtsx",  
        null);  
      Variables pkgVars = pkg.Variables;  
      Variable myVar = pkg.Variables.Add("myCustomVar", false, "User", "3");  
      foreach (Variable pkgVar in pkgVars)  
      {  
        Console.WriteLine("Variable: {0}, {1}, {2}", pkgVar.Name,  
          pkgVar.DataType, pkgVar.Value.ToString());  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim app As Application = New Application()  
    ' Load a sample package that contains a variable that sets the file name.  
    Dim pkg As Package = app.LoadPackage( _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\CaptureDataLineage Sample\CaptureDataLineage\CaptureDataLineage.dtsx", _  
      Nothing)  
    Dim pkgVars As Variables = pkg.Variables  
    Dim myVar As Variable = pkg.Variables.Add("myCustomVar", False, "User", "3")  
    Dim pkgVar As Variable  
    For Each pkgVar In pkgVars  
      Console.WriteLine("Variable: {0}, {1}, {2}", pkgVar.Name, _  
        pkgVar.DataType, pkgVar.Value.ToString())  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **Salida de ejemplo:**  
  
 `Variable: CancelEvent, Int32, 0`  
  
 `Variable: CreationDate, DateTime, 4/18/2003 11:57:00 AM`  
  
 `Variable: CreatorComputerName, String,`  
  
 `Variable: CreatorName, String,`  
  
 `Variable: ExecutionInstanceGUID, String, {237AB5A4-7E59-4FC9-8D61-E8F20363DF25}`  
  
 `Variable: FileName, String, Junk`  
  
 `Variable: InteractiveMode, Boolean, False`  
  
 `Variable: LocaleID, Int32, 1033`  
  
 `Variable: MachineName, String, MYCOMPUTERNAME`  
  
 `Variable: myCustomVar, String, 3`  
  
 `Variable: OfflineMode, Boolean, False`  
  
 `Variable: PackageID, String, {F0D2E396-A6A5-42AE-9467-04CE946A810C}`  
  
 `Variable: PackageName, String, DTSPackage1`  
  
 `Variable: StartTime, DateTime, 1/28/2005 7:55:39 AM`  
  
 `Variable: UserName, String, <domain>\<userid>`  
  
 `Variable: VersionBuild, Int32, 198`  
  
 `Variable: VersionComments, String,`  
  
 `Variable: VersionGUID, String, {90E105B4-B4AF-4263-9CBD-C2050C2D6148}`  
  
 `Variable: VersionMajor, Int32, 1`  
  
 `Variable: VersionMinor, Int32, 0`  
  
 Tenga en cuenta que todas las variables con ámbito en el **System** espacio de nombres están disponibles para el paquete. Para más información, consulte [System Variables](../../integration-services/system-variables.md).  
  
## <a name="namespaces"></a>Espacios de nombres  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) proporciona dos espacios de nombres predeterminados donde residen las variables; **Usuario** y **System** espacios de nombres. De forma predeterminada, cualquier variable personalizada creada por el programador se agrega a la **usuario** espacio de nombres. Las variables del sistema residen en la **System** espacio de nombres. Puede crear espacios de nombres adicionales distintos de la **usuario** espacio de nombres para contener variables personalizadas y puede cambiar el nombre de la **usuario** espacio de nombres, pero no puede agregar ni modificar las variables en el **System** espacio de nombres, o asignar variables del sistema a otro espacio de nombres.  
  
 Las variables del sistema que están disponibles difieren en función del tipo de contenedor. Para obtener una lista de las variables del sistema disponibles para paquetes, contenedores, tareas y controladores de eventos, vea [las Variables del sistema](../../integration-services/system-variables.md).  
  
## <a name="value"></a>Value  
 El valor de una variable personalizada puede ser un literal o una expresión:  
  
-   Si desea que la variable contenga un valor literal, establezca el valor de su propiedad <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A>.  
  
-   Si desea que la variable para contener una expresión, por lo que puede usar los resultados de la expresión como su valor, establezca la <xref:Microsoft.SqlServer.Dts.Runtime.Variable.EvaluateAsExpression%2A> propiedad de la variable a **true**y escriba una expresión en el <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Expression%2A> propiedad. En el tiempo de ejecución, se evalúa la expresión, y el resultado de la evaluación de la expresión se usa como el valor de la variable. Por ejemplo, si la propiedad de expresión de una variable es `"100 * 2""100 * 2"` , la variable se evalúa como un valor de 200.  
  
 Para una variable, no puede establecer explícitamente el valor de su <xref:Microsoft.SqlServer.Dts.Runtime.Variable.DataType%2A>. El valor <xref:Microsoft.SqlServer.Dts.Runtime.Variable.DataType%2A> se deduce del valor inicial asignado a la variable y ya no se puede cambiar. Para obtener más información acerca de los tipos de datos de la variable, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 En el ejemplo de código siguiente se crea una nueva variable, se establece <xref:Microsoft.SqlServer.Dts.Runtime.Variable.EvaluateAsExpression%2A> a **true**, asigna la expresión `"100 * 2"` para la propiedad expression de la variable y, a continuación, genera el valor de la variable.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package pkg = new Package();  
      Variable v100 = pkg.Variables.Add("myVar", false, "", 1);  
      v100.EvaluateAsExpression = true;  
      v100.Expression = "100 * 2";  
      Console.WriteLine("Expression for myVar: {0}",   
        v100.Properties["Expression"].GetValue(v100));  
      Console.WriteLine("Value of myVar: {0}", v100.Value.ToString());  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim pkg As Package = New Package  
    Dim v100 As Variable = pkg.Variables.Add("myVar", False, "", 1)  
    v100.EvaluateAsExpression = True  
    v100.Expression = "100 * 2"  
    Console.WriteLine("Expression for myVar: {0}", _  
      v100.Properties("Expression").GetValue(v100))  
    Console.WriteLine("Value of myVar: {0}", v100.Value.ToString)  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **Salida de ejemplo:**  
  
 `Expression for myVar: 100 * 2`  
  
 `Value of myVar: 200`  
  
 La expresión debe ser una expresión válida que use la sintaxis de expresiones de [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Los literales se permiten en expresiones variables, además de los operadores y funciones que proporciona la sintaxis de la expresión, pero las expresiones no pueden hacer referencia a otras variables o columnas. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
## <a name="configuration-files"></a>Archivos de configuración  
 Si un archivo de configuración incluye una variable personalizada, la variable puede estar actualizada en tiempo de ejecución. Esto significa que cuando el paquete se ejecuta, se reemplaza el valor de la variable originalmente en el paquete con un nuevo valor del archivo de configuración. Esta técnica del reemplazo es útil cuando se implementa un paquete en varios servidores que requieren distintos valores de variable. Por ejemplo, una variable puede especificar el número de veces que un **bucles Foreach** contenedor repite su flujo de trabajo, o lista de los destinatarios que un controlador de eventos envía un correo electrónico cuando se produce un error o cambiar el número de errores que pueden producirse antes de que se produce un error en el paquete. Estas variables se proporcionan de forma dinámica en archivos de configuración para cada entorno. Por consiguiente, en archivos de configuración únicamente se permiten variables de lectura/escritura. Para obtener más información, vea [Crear configuraciones de paquetes](../../integration-services/packages/create-package-configurations.md).  
  
## <a name="see-also"></a>Vea también  
 [Integration Services &#40; SSIS &#41; Variables](../../integration-services/integration-services-ssis-variables.md)   
 [Usar Variables en paquetes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  

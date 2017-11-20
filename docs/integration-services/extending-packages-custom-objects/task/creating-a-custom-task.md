---
title: Crear una tarea personalizada | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom tasks [Integration Services], creating
ms.assetid: 42965c09-1782-4cdb-9ce1-216af4c23e0a
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3d804ae69154913f4c5239a6bec304f14c4b856d
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="creating-a-custom-task"></a>Crear una tarea personalizada
  Los pasos necesarios para crear una tarea personalizada son similares a los pasos para crear cualquier otro objeto personalizado para [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]:  
  
-   Cree una clase nueva que herede de la clase base. En una tarea, la clase base es <xref:Microsoft.SqlServer.Dts.Runtime.Task>.  
  
-   Aplique el atributo que identifica el tipo de objeto para la clase. En una tarea, el atributo es <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>.  
  
-   Reemplace la implementación de métodos y propiedades de la clase base. En una tarea, incluyen los métodos <xref:Microsoft.SqlServer.Dts.Runtime.Task.Validate%2A> y <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>.  
  
-   Si lo desea, desarrolle una interfaz de usuario personalizada. En una tarea, esto requiere una clase que implemente la interfaz <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI>.  
  
## <a name="getting-started-with-a-custom-task"></a>Introducción a una tarea personalizada  
  
### <a name="creating-projects-and-classes"></a>Crear proyectos y clases  
 Dado que todas las tareas administradas se derivan de la clase base <xref:Microsoft.SqlServer.Dts.Runtime.Task>, el primer paso al crear una tarea personalizada consiste en crear un proyecto de bibliotecas de clases en el lenguaje de programación administrado que prefiera y crear una clase que herede de la clase base. En esta clase derivada se invalidarán los métodos y las propiedades de la clase base para implementar la funcionalidad personalizada.  
  
 En la misma solución, cree un segundo proyecto de bibliotecas de clases para la interfaz de usuario personalizada. Se recomienda utilizar un ensamblado independiente para la interfaz de usuario a fin de facilitar la implementación, ya que le permite actualizar y volver a implementar la tarea o su interfaz de usuario de forma independiente.  
  
 Configure ambos proyectos para firmar los ensamblados que se generarán en tiempo de compilación mediante un archivo de clave de nombre seguro.  
  
### <a name="applying-the-dtstask-attribute"></a>Aplicar el atributo DtsTask  
 Aplique el atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> a la clase que ha creado para identificarla como una tarea. Este atributo proporciona información en tiempo de diseño, como el nombre, la descripción y el tipo de tarea de la tarea.  
  
 Utilice la propiedad <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.UITypeName%2A> para vincular la tarea a su interfaz de usuario personalizada. Para obtener el token de clave pública que se requiere para esta propiedad, puede usar **sn.exe -t** para mostrar el token de clave pública del archivo de par de claves (.snk) que se va a usar para firmar el ensamblado de la interfaz de usuario.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
namespace Microsoft.SSIS.Samples  
{  
  [DtsTask  
  (  
   DisplayName = "MyTask",  
   IconResource = "MyTask.MyTaskIcon.ico",  
   UITypeName = "My Custom Task," +  
   "Version=1.0.0.0," +  
   "Culture = Neutral," +  
   "PublicKeyToken = 12345abc6789de01",  
   TaskType = "PackageMaintenance",  
   TaskContact = "MyTask; company name; any other information",  
   RequiredProductLevel = DTSProductLevel.None  
   )]  
  public class MyTask : Task  
  {  
    // Your code here.  
  }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
  
<DtsTask(DisplayName:="MyTask", _  
 IconResource:="MyTask.MyTaskIcon.ico", _  
 UITypeName:="My Custom Task," & _  
 "Version=1.0.0.0,Culture=Neutral," & _  
 "PublicKeyToken=12345abc6789de01", _  
 TaskType:="PackageMaintenance", _  
 TaskContact:="MyTask; company name; any other information", _  
 RequiredProductLevel:=DTSProductLevel.None)> _  
Public Class MyTask  
  Inherits Task  
  
  ' Your code here.  
  
End Class 'MyTask  
```  
  
## <a name="building-deploying-and-debugging-a-custom-task"></a>Generar, implementar y depurar una tarea personalizada  
 Los pasos para generar, implementar y depurar una tarea personalizada en [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] son similares a los pasos necesarios en otros tipos de objetos personalizados. Para obtener más información, consulte [Building, Deploying and Debugging Custom Objects](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).  
  
## <a name="see-also"></a>Vea también  
 [Crear una tarea personalizada](../../../integration-services/extending-packages-custom-objects/task/creating-a-custom-task.md)   
 [Codificar una tarea personalizada](../../../integration-services/extending-packages-custom-objects/task/coding-a-custom-task.md)   
 [Desarrollar una interfaz de usuario para una tarea personalizada](../../../integration-services/extending-packages-custom-objects/task/developing-a-user-interface-for-a-custom-task.md)  
  
  


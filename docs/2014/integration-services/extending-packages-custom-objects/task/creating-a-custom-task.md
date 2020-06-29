---
title: Crear una tarea personalizada | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom tasks [Integration Services], creating
ms.assetid: 42965c09-1782-4cdb-9ce1-216af4c23e0a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: dc1aeb650810f9b6d580dabcd22091a2e1eb9d49
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85427262"
---
# <a name="creating-a-custom-task"></a>Crear una tarea personalizada
  Los pasos necesarios para crear una tarea personalizada son similares a los pasos para crear cualquier otro objeto personalizado para [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]:  
  
-   Cree una clase nueva que herede de la clase base. En una tarea, la clase base es <xref:Microsoft.SqlServer.Dts.Runtime.Task>.  
  
-   Aplique el atributo que identifica el tipo de objeto para la clase. En una tarea, el atributo es <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>.  
  
-   Invalide la implementación de los métodos y las propiedades de la clase base. En una tarea, incluyen los métodos <xref:Microsoft.SqlServer.Dts.Runtime.Task.Validate%2A> y <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>.  
  
-   Si lo desea, desarrolle una interfaz de usuario personalizada. En una tarea, esto requiere una clase que implemente la interfaz <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI>.  
  
## <a name="getting-started-with-a-custom-task"></a>Introducción a una tarea personalizada  
  
### <a name="creating-projects-and-classes"></a>Crear proyectos y clases  
 Dado que todas las tareas administradas se derivan de la clase base <xref:Microsoft.SqlServer.Dts.Runtime.Task>, el primer paso al crear una tarea personalizada consiste en crear un proyecto de bibliotecas de clases en el lenguaje de programación administrado que prefiera y crear una clase que herede de la clase base. En esta clase derivada se invalidarán los métodos y las propiedades de la clase base para implementar la funcionalidad personalizada.  
  
 En la misma solución, cree un segundo proyecto de bibliotecas de clases para la interfaz de usuario personalizada. Se recomienda utilizar un ensamblado independiente para la interfaz de usuario a fin de facilitar la implementación, ya que le permite actualizar y volver a implementar la tarea o su interfaz de usuario de forma independiente.  
  
 Configure ambos proyectos para firmar los ensamblados que se generarán en tiempo de compilación mediante un archivo de clave de nombre seguro.  
  
### <a name="applying-the-dtstask-attribute"></a>Aplicar el atributo DtsTask  
 Aplique el atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> a la clase que ha creado para identificarla como una tarea. Este atributo proporciona información en tiempo de diseño, como el nombre, la descripción y el tipo de tarea de la tarea.  
  
 Utilice la propiedad <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.UITypeName%2A> para vincular la tarea a su interfaz de usuario personalizada. Para obtener el token de clave pública necesario para esta propiedad, puede usar **sn.exe -t** con el fin de mostrar el token de clave pública del archivo de pares de claves (.snk) que quiere usar para firmar el ensamblado de la interfaz de usuario.  
  
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
 Los pasos para generar, implementar y depurar una tarea personalizada en [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] son similares a los pasos necesarios en otros tipos de objetos personalizados. Para obtener más información, consulte [Generar, implementar y depurar objetos personalizados](../building-deploying-and-debugging-custom-objects.md).  
  
![Integration Services icono (pequeño)](../../media/dts-16.gif "Icono de Integration Services (pequeño)")  **Manténgase al día con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Consulte también  
 [Crear una tarea personalizada](creating-a-custom-task.md)   
 [Codificar una tarea personalizada](coding-a-custom-task.md)   
 [Desarrollar una interfaz de usuario para una tarea personalizada](developing-a-user-interface-for-a-custom-task.md)  
  
  

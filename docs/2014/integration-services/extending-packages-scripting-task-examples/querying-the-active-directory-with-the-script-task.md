---
title: Consultar Active Directory con la tarea Script | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], Active Directory access
- SSIS Script task, Active Directory access
- Script task [Integration Services], examples
- Active Directory [Integration Services]
ms.assetid: a88fefbb-9ea2-4a86-b836-e71315bac68e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bbcea29ad75eb84b9c8099e5998e307ecbd7943c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62895034"
---
# <a name="querying-the-active-directory-with-the-script-task"></a>Consultar Active Directory con la tarea Script
  Las aplicaciones de procesamiento de datos empresariales, como los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], a menudo tienen que procesar los datos de forma distinta según la categoría, el puesto u otras características de los empleados almacenados en Active Directory. Active Directory es un servicio de directorios de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows que proporciona un almacén centralizado de metadatos, no solamente acerca de los usuarios, sino también acerca de otros recursos de la organización, como los equipos y las impresoras. El espacio de nombres `System.DirectoryServices` de Microsoft .NET Framework proporciona las clases para trabajar con Active Directory, con el fin de ayudarle a dirigir el flujo de trabajo de procesamiento de datos basándose en la información que almacena.  
  
> [!NOTE]  
>  Si desea crear una tarea que pueda reutilizar más fácilmente en varios paquetes, considere la posibilidad de utilizar el código de este ejemplo de tarea Script como punto inicial de una tarea personalizada. Para más información, vea [Desarrollar una tarea personalizada](../extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Descripción  
 En el ejemplo siguiente se recupera el nombre, el puesto y el número de teléfono de un empleado de Active Directory basándose en el valor de la variable `email`, que contiene la dirección de correo electrónico del empleado. Las restricciones de precedencia en el paquete utilizan la información recuperada para determinar, por ejemplo, si se va a enviar un mensaje de correo electrónico de prioridad baja o una página prioritaria, basándose en el puesto del empleado.  
  
#### <a name="to-configure-this-script-task-example"></a>Para configurar este ejemplo de tarea Script  
  
1.  Cree las tres variable de cadena `email`, `name` y `title`. Escriba una dirección de correo electrónico corporativa válida como el valor de la variable `email`.  
  
2.  En el **Script** página de la **Editor de la tarea Script**, agregar el `email` variable a la `ReadOnlyVariables` propiedad.  
  
3.  Agregue las variables `name` y `title` a la propiedad `ReadWriteVariables`.  
  
4.  En el proyecto de script, agregue una referencia a la `System.DirectoryServices` espacio de nombres.  
  
5.  . En el código, utilice una instrucción `Imports` para importar el espacio de nombres `DirectoryServices`.  
  
> [!NOTE]  
>  Para ejecutar correctamente este script, la empresa debe utilizar Active Directory en la red y almacenar la información de empleado que este ejemplo utiliza.  
  
### <a name="code"></a>Código  
  
```vb  
Public Sub Main()  
  
    Dim directory As DirectoryServices.DirectorySearcher  
    Dim result As DirectoryServices.SearchResult  
    Dim email As String  
  
    email = Dts.Variables("email").Value.ToString  
  
    Try  
        directory = New _  
            DirectoryServices.DirectorySearcher("(mail=" & email & ")")  
        result = directory.FindOne  
        Dts.Variables("name").Value = _  
            result.Properties("displayname").ToString  
        Dts.Variables("title").Value = _  
            result.Properties("title").ToString  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, _  
            "Script Task Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
```  
  
```csharp  
public void Main()  
{  
    //  
    DirectorySearcher directory;  
    SearchResult result;  
    string email;  
  
    email = (string)Dts.Variables["email"].Value;  
  
    try  
    {  
        directory = new DirectorySearcher("(mail=" + email + ")");  
        result = directory.FindOne();  
        Dts.Variables["name"].Value = result.Properties["displayname"].ToString();  
        Dts.Variables["title"].Value = result.Properties["title"].ToString();  
        Dts.TaskResult = (int)ScriptResults.Success;  
    }  
    catch (Exception ex)  
    {  
        Dts.Events.FireError(0, "Script Task Example", ex.Message + "\n" + ex.StackTrace, String.Empty, 0);  
        Dts.TaskResult = (int)ScriptResults.Failure;  
    }  
  
}  
```  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Artículo técnico, [Procesar la información de Active Directory en SSIS](https://go.microsoft.com/fwlink/?LinkId=199588), en social.technet.microsoft.com  
  
![Icono de Integration Services (pequeño)](../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
  

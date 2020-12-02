---
description: Consultar Active Directory con la tarea Script
title: Consultar Active Directory con la tarea Script | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 98f71295a8df150b7430806c35aae47cca0bc613
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/26/2020
ms.locfileid: "88430397"
---
# <a name="querying-the-active-directory-with-the-script-task"></a>Consultar Active Directory con la tarea Script

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Las aplicaciones de procesamiento de datos empresariales, como los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], a menudo tienen que procesar los datos de forma distinta según la categoría, el puesto u otras características de los empleados almacenados en Active Directory. Active Directory es un servicio de directorios de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows que proporciona un almacén centralizado de metadatos, no solamente acerca de los usuarios, sino también acerca de otros recursos de la organización, como los equipos y las impresoras. El espacio de nombres **System.DirectoryServices** de Microsoft .NET Framework proporciona las clases para trabajar con Active Directory, con el fin de ayudarle a dirigir el flujo de trabajo de procesamiento de datos basándose en la información que almacena.  
  
> [!NOTE]  
>  Si desea crear una tarea que pueda reutilizar más fácilmente en varios paquetes, considere la posibilidad de utilizar el código de este ejemplo de tarea Script como punto inicial de una tarea personalizada. Para más información, vea [Desarrollar una tarea personalizada](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Descripción  
 En el ejemplo siguiente se recupera el nombre, el puesto y el número de teléfono de un empleado de Active Directory basándose en el valor de la variable `email`, que contiene la dirección de correo electrónico del empleado. Las restricciones de precedencia en el paquete utilizan la información recuperada para determinar, por ejemplo, si se va a enviar un mensaje de correo electrónico de prioridad baja o una página prioritaria, basándose en el puesto del empleado.  
  
#### <a name="to-configure-this-script-task-example"></a>Para configurar este ejemplo de tarea Script  
  
1.  Cree las tres variable de cadena `email`, `name` y `title`. Escriba una dirección de correo electrónico corporativa válida como el valor de la variable `email`.  
  
2.  En la página **Script** del **Editor de la tarea Script**, agregue la variable `email` a la propiedad **ReadOnlyVariables**.  
  
3.  Agregue las variables `name` y `title` a la propiedad **ReadWriteVariables**.  
  
4.  Agregue una referencia al espacio de nombres **System.DirectoryServices** en el proyecto de script.  
  
5.  . En el código, utilice una instrucción **Imports** para importar el espacio de nombres **DirectoryServices**.  
  
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
  
  

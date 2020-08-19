---
description: Detectar un archivo plano vacío con la tarea Script
title: Detectar un archivo plano vacío con la tarea Script | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- flat files
- Script task [Integration Services], empty flat files
- SSIS Script task, empty flat files
- Script task [Integration Services], examples
ms.assetid: 1b4defb8-886a-483d-8056-d1b91d37bc90
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d5c1c5473eb307480b772d2cecd31b3ebb2a9bed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430437"
---
# <a name="detecting-an-empty-flat-file-with-the-script-task"></a>Detectar un archivo plano vacío con la tarea Script

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  El origen de archivo plano no determina si un archivo de este tipo contiene filas de datos antes de intentar procesarlo. Puede que desee mejorar la eficacia de un paquete (sobre todo un paquete que recorre en iteración numerosos archivos planos) mediante la omisión de archivos que no contienen filas de datos. La tarea Script puede buscar un archivo plano vacío antes de que el paquete comience a procesar el flujo de datos.  
  
> [!NOTE]  
>  Si desea crear una tarea que pueda reutilizar más fácilmente en varios paquetes, considere la posibilidad de utilizar el código de este ejemplo de tarea Script como punto inicial de una tarea personalizada. Para más información, vea [Desarrollar una tarea personalizada](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Descripción  
 En el ejemplo siguiente se utilizan métodos del espacio de nombres **System.IO** para probar el archivo plano especificado en un administrador de conexiones de archivos planos a fin de determinar si el archivo está vacío o si solamente contiene filas esperadas que no son de datos, como encabezados de columna o una línea vacía. En primer lugar, el script comprueba el tamaño del archivo; si el tamaño es de cero bytes, el archivo está vacío. Si el tamaño de archivo es mayor que cero, el script lee las líneas del archivo hasta que no haya más líneas o hasta que el número de líneas supere el número esperado de filas que no son de datos. Si el número de líneas del archivo es menor o igual que el número esperado de filas que no son de datos, se considera que el archivo está vacío. El resultado se devuelve como valor booleano en una variable de usuario, cuyo valor puede utilizarse para la bifurcación del flujo de control del paquete. El método **FireInformation** también muestra el resultado en la ventana **Salida** de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA).  
  
#### <a name="to-configure-this-script-task-example"></a>Para configurar este ejemplo de tarea Script  
  
1.  Cree y configure un administrador de conexiones de archivos planos denominado **EmptyFlatFileTest**.  
  
2.  Cree una variable de entero denominada `FFNonDataRows` y establezca su valor en el número esperado de filas que no son de datos del archivo plano.  
  
3.  Cree una variable booleana denominada `FFIsEmpty`.  
  
4.  Agregue la variable `FFNonDataRows` a la propiedad **ReadOnlyVariables** de la tarea Script.  
  
5.  Agregue la variable `FFIsEmpty` a la propiedad **ReadWriteVariables** de la tarea Script.  
  
6.  Importe el espacio de nombres **System.IO** en su código.  
  
 Si recorre en iteración archivos con un enumerador Foreach File, en lugar de utilizar solamente un administrador de conexiones de archivos planos, tendrá que modificar el código de ejemplo siguiente para obtener el nombre de archivo y la ruta de acceso de la variable donde se almacena el valor enumerado y no del administrador de conexiones.  
  
### <a name="code"></a>Código  
  
```vb  
Public Sub Main()  
  
  Dim nonDataRows As Integer = _  
      DirectCast(Dts.Variables("FFNonDataRows").Value, Integer)  
  Dim ffConnection As String = _  
      DirectCast(Dts.Connections("EmptyFlatFileTest").AcquireConnection(Nothing), _  
      String)  
  Dim flatFileInfo As New FileInfo(ffConnection)  
  ' If file size is 0 bytes, flat file does not contain data.  
  Dim fileSize As Long = flatFileInfo.Length  
  If fileSize > 0 Then  
    Dim lineCount As Integer = 0  
    Dim line As String  
    Dim fsFlatFile As New StreamReader(ffConnection)  
    Do Until fsFlatFile.EndOfStream  
      line = fsFlatFile.ReadLine  
      lineCount += 1  
      ' If line count > expected number of non-data rows,  
      '  flat file contains data (default value).  
      If lineCount > nonDataRows Then  
        Exit Do  
      End If  
      ' If line count <= expected number of non-data rows,  
      '  flat file does not contain data.  
      If lineCount <= nonDataRows Then  
        Dts.Variables("FFIsEmpty").Value = True  
      End If  
    Loop  
  Else  
    Dts.Variables("FFIsEmpty").Value = True  
  End If  
  
  Dim fireAgain As Boolean = False  
  Dts.Events.FireInformation(0, "Script Task", _  
      String.Format("{0}: {1}", ffConnection, _  
      Dts.Variables("FFIsEmpty").Value.ToString), _  
      String.Empty, 0, fireAgain)  
  
  Dts.TaskResult = ScriptResults.Success  
  
End Sub  
```  
  
```csharp  
public void Main()  
        {  
  
            int nonDataRows = (int)(Dts.Variables["FFNonDataRows"].Value);  
            string ffConnection = (string)(Dts.Connections["EmptyFlatFileTest"].AcquireConnection(null) as String);  
            FileInfo flatFileInfo = new FileInfo(ffConnection);  
            // If file size is 0 bytes, flat file does not contain data.  
            long fileSize = flatFileInfo.Length;  
            if (fileSize > 0)  
            {  
  
                int lineCount = 0;  
                string line;  
                StreamReader fsFlatFile = new StreamReader(ffConnection);  
                while (!(fsFlatFile.EndOfStream))  
                {  
                    Console.WriteLine (fsFlatFile.ReadLine());  
                    lineCount += 1;  
                    // If line count > expected number of non-data rows,  
                    //  flat file contains data (default value).  
                    if (lineCount > nonDataRows)  
                    {  
                        break;  
                    }  
                    // If line count <= expected number of non-data rows,  
                    //  flat file does not contain data.  
                    if (lineCount <= nonDataRows)  
                    {  
                        Dts.Variables["FFIsEmpty"].Value = true;  
                    }  
                }  
            }  
            else  
            {  
                Dts.Variables["FFIsEmpty"].Value = true;  
            }  
  
            bool fireAgain = false;  
            Dts.Events.FireInformation(0, "Script Task", String.Format("{0}: {1}", ffConnection, Dts.Variables["FFIsEmpty"].Value), String.Empty, 0, ref fireAgain);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
```  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplos de tarea Script](../../integration-services/extending-packages-scripting-task-examples/script-task-examples.md)  
  
  

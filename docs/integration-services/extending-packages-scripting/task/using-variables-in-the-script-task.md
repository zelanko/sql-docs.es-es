---
title: Uso de Variables en la tarea Script | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Foreach Loop containers
- Script task [Integration Services], variables
- scripts [Integration Services], variables
- Variables property
- Variable object
- SSIS Script task, variables
- variables [Integration Services], Script task
ms.assetid: 593b5961-4bfa-4ce1-9531-a251c34e89d3
caps.latest.revision: 63
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ccfd7ce8e8f53d12dac3b021d5f62bd03947413d
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="using-variables-in-the-script-task"></a>Utilizar variables en la tarea Script
  Las variables permiten que la tarea Script intercambie datos con otros objetos del paquete. Para más información, vea [Integration Services &#40;SSIS&#41; Variables](../../../integration-services/integration-services-ssis-variables.md).  
  
 La tarea de secuencia de comandos utiliza el <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> propiedad de la **Dts** objeto para leer y escribir en <xref:Microsoft.SqlServer.Dts.Runtime.Variable> objetos del paquete.  
  
> [!NOTE]  
>  El <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A> propiedad de la <xref:Microsoft.SqlServer.Dts.Runtime.Variable> clase es de tipo **objeto**. Dado que la tarea Script tiene **Option Strict** habilitado, debe convertir el <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A> propiedad al tipo adecuado antes de utilizarla.  
  
 Agregar variables existentes a la <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadOnlyVariables%2A> y <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadWriteVariables%2A> se enumeran en la **Editor de la tarea de secuencia de comandos** para que estén disponibles en el script personalizado. Tenga presente que los nombres de variable distinguen entre mayúsculas y minúsculas. Dentro de la secuencia de comandos, tener acceso a las variables de ambos tipos a través de la <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> propiedad de la **Dts** objeto. Use la **valor** propiedad para leer y escribir en las variables individuales. La tarea Script administra de forma transparente el bloqueo a medida que el script lee y modifica los valores de las variables.  
  
 Puede utilizar el método <xref:Microsoft.SqlServer.Dts.Runtime.Variables.Contains%2A> de la colección <xref:Microsoft.SqlServer.Dts.Runtime.Variables> que devuelve la propiedad <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> para comprobar la existencia de una variable antes de utilizarla en el código.  
  
 También puede usar el <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A> propiedad (Dts.VariableDispenser) para trabajar con variables en la tarea de secuencia de comandos. Al utilizar <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A>, debe administrar la semántica de bloqueo y la conversión de tipos de datos para los valores de variables en su propio código. Puede que necesite utilizar la propiedad <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A> en lugar de la propiedad <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> si desea trabajar con una variable que no está disponible en tiempo de diseño pero que se crea mediante programación en tiempo de ejecución.  
  
## <a name="using-the-script-task-within-a-foreach-loop-container"></a>Utilizar la tarea Script dentro de un contenedor de bucles Foreach  
 Cuando una tarea Script se ejecuta repetidamente dentro de un contenedor de bucles Foreach, normalmente el script necesita trabajar con el contenido del elemento actual en el enumerador. Por ejemplo, al utilizar un enumerador de archivos Foreach, el script necesita conocer el nombre del archivo actual; al utilizar un enumerador de ADO para Foreach, el script necesita conocer el contenido de las columnas en la fila actual de datos.  
  
 Las variables consiguen que sea posible esta comunicación entre el contenedor de bucles Foreach y la tarea Script. En el **asignaciones de variables** página de la **Editor de bucles Foreach**, asignar variables a cada elemento de datos que devuelven un único elemento enumerado. Por ejemplo, un enumerador de archivos Foreach solamente devuelve un nombre de archivo en Índice 0 y por tanto solamente requiere una asignación de variable, en tanto que un enumerador que devuelve varias columnas de datos en cada fila requiere que asigne una variable diferente a cada columna que desea utilizar en la tarea Script.  
  
 Después de asignar los elementos enumerados a las variables, debe agregar las variables asignadas a la **ReadOnlyVariables** propiedad en el **Script** página de la **Editor de la tarea de secuencia de comandos** para que estén disponibles en la secuencia de comandos. Para obtener un ejemplo de una tarea de secuencia de comandos dentro de un contenedor de bucles Foreach que procesa los archivos de imagen en una carpeta, consulte [trabajar con imágenes con la tarea de secuencia de comandos](../../../integration-services/extending-packages-scripting-task-examples/working-with-images-with-the-script-task.md).  
  
## <a name="variables-example"></a>Ejemplo de variables  
 En el ejemplo siguiente se muestra cómo obtener acceso y utilizar las variables en una tarea Script para determinar la ruta de acceso de flujo de trabajo del paquete. El ejemplo se supone que ha creado las variables de entero denominadas `CustomerCount` y `MaxRecordCount` y agregarlos a la **ReadOnlyVariables** colección en la **Editor de la tarea de secuencia de comandos**. La variable `CustomerCount` contiene el número de registros del cliente que se van a importar. Si su valor es mayor que el valor de `MaxRecordCount`, la tarea Script informa del error. Cuando se produce un error porque se ha superado el umbral `MaxRecordCount`, la ruta de acceso de error del flujo de trabajo puede implementar cualquier limpieza necesaria.  
  
 Para compilar correctamente el ejemplo, debe agregar una referencia al ensamblado Microsoft.SqlServer.ScriptTask.  
  
```vb  
Public Sub Main()  
  
    Dim customerCount As Integer  
    Dim maxRecordCount As Integer  
  
    If Dts.Variables.Contains("CustomerCount") = True AndAlso _  
        Dts.Variables.Contains("MaxRecordCount") = True Then  
  
        customerCount = _  
            CType(Dts.Variables("CustomerCount").Value, Integer)  
        maxRecordCount = _  
            CType(Dts.Variables("MaxRecordCount").Value, Integer)  
  
    End If  
  
    If customerCount > maxRecordCount Then  
            Dts.TaskResult = ScriptResults.Failure  
    Else  
            Dts.TaskResult = ScriptResults.Success  
    End If  
  
End Sub  
```  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Runtime;  
  
public class ScriptMain  
{  
  
    public void Main()  
    {  
        int customerCount;  
        int maxRecordCount;  
  
        if (Dts.Variables.Contains("CustomerCount")==true&&Dts.Variables.Contains("MaxRecordCount")==true)  
  
        {  
            customerCount = (int) Dts.Variables["CustomerCount"].Value;  
            maxRecordCount = (int) Dts.Variables["MaxRecordCount"].Value;  
  
        }  
  
        if (customerCount>maxRecordCount)  
        {  
            Dts.TaskResult = (int)ScriptResults.Failure;  
        }  
        else  
        {  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
  
    }  
  
}  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Integration Services &#40; SSIS &#41; Variables](../../../integration-services/integration-services-ssis-variables.md)   
 [Usar Variables en paquetes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  


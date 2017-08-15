---
title: "Supervisión de contadores de rendimiento con la tarea Script | Documentos de Microsoft"
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
helpviewer_keywords:
- performance counters [Integration Services]
- SSIS Script task, performance counters
- custom performance counters [Integration Services]
- Script task [Integration Services], examples
- Script task [Integration Services], performance counters
- counters [Integration Services]
ms.assetid: 86609bf1-cae6-435e-a58d-41bdfc521e94
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: fd733f7d2fdf9c5d1181df6e7856d729e9a58026
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="monitoring-performance-counters-with-the-script-task"></a>Supervisar los contadores de rendimiento con la tarea Script
  Los administradores quizá tengan que supervisar el rendimiento de los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que realizan transformaciones complejas en grandes volúmenes de datos. El **System.Diagnostics** espacio de nombres de la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] proporciona clases para el uso de contadores de rendimiento existentes y para crear sus propios contadores de rendimiento.  
  
 Los contadores de rendimiento almacenan información sobre el rendimiento de la aplicación que puede utilizar para analizar el rendimiento del software a lo largo del tiempo. Contadores de rendimiento pueden supervisarse localmente o de forma remota mediante el uso de la **Monitor de rendimiento** herramienta. Puede almacenar los valores de los contadores de rendimiento en variables para la bifurcación del flujo de control posterior en el paquete.  
  
 Como alternativa al uso de contadores de rendimiento, puede generar el <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A> eventos a través de la <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> propiedad de la **Dts** objeto. El evento <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A> devuelve el progreso incremental e información del porcentaje completado al módulo ejecutable de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
> [!NOTE]  
>  Si desea crear una tarea que pueda reutilizar más fácilmente en varios paquetes, considere la posibilidad de utilizar el código de este ejemplo de tarea Script como punto inicial de una tarea personalizada. Para más información, vea [Desarrollar una tarea personalizada](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Description  
 En el ejemplo siguiente se crea un contador de rendimiento personalizado y se incrementa el contador. Primero, el ejemplo determina si el contador de rendimiento ya existe. Si el contador de rendimiento no se ha creado, el script llama el **crear** método de la **PerformanceCounterCategory** objeto para crearla. Una vez creado el contador de rendimiento, el script incrementa el contador. Por último, en el ejemplo se sigue la práctica recomendada de llamar al método el **cerrar** método en el contador de rendimiento cuando ya no es necesario.  
  
> [!NOTE]  
>  Crear una nueva categoría de contador de rendimiento y el contador de rendimiento requiere derechos administrativos. Además, la nueva categoría y el contador se conservan en el equipo después de la creación.  
  
#### <a name="to-configure-this-script-task-example"></a>Para configurar este ejemplo de tarea Script  
  
-   Use un **importaciones** instrucción en el código para importar el **System.Diagnostics** espacio de nombres.  
  
### <a name="example-code"></a>Código de ejemplo  
  
```vb  
Public Sub Main()  
  
    Dim myCounter As PerformanceCounter  
  
    Try  
        'Create the performance counter if it does not already exist.  
        If Not _  
        PerformanceCounterCategory.Exists("TaskExample") Then  
            PerformanceCounterCategory.Create("TaskExample", _  
                "Task Performance Counter Example", "Iterations", _  
                "Number of times this task has been called.")  
        End If  
  
        'Initialize the performance counter.  
        myCounter = New PerformanceCounter("TaskExample", _  
            "Iterations", String.Empty, False)  
  
        'Increment the performance counter.  
        myCounter.Increment()  
  
         myCounter.Close()  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, _  
            "Task Performance Counter Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
```  
  
```csharp  
  
public class ScriptMain  
{  
  
public void Main()  
        {  
  
            PerformanceCounter myCounter;  
  
            try  
            {  
                //Create the performance counter if it does not already exist.  
                if (!PerformanceCounterCategory.Exists("TaskExample"))  
                {  
                    PerformanceCounterCategory.Create("TaskExample", "Task Performance Counter Example", "Iterations", "Number of times this task has been called.");  
                }  
  
                //Initialize the performance counter.  
                myCounter = new PerformanceCounter("TaskExample", "Iterations", String.Empty, false);  
  
                //Increment the performance counter.  
                myCounter.Increment();  
  
                myCounter.Close();  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                Dts.Events.FireError(0, "Task Performance Counter Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
  
```  


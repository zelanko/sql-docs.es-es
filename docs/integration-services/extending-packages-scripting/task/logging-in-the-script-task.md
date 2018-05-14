---
title: Registrar en la tarea Script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: extending-packages-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- logs [Integration Services], scripts
- Integration Services packages, logs
- Log method
- SSIS Script task, logs
- Script task [Integration Services], logs
- packages [Integration Services], logs
ms.assetid: 2e11fc15-df18-4309-bd2d-fc58aa4b9b7a
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9691e6b27fd3a0c072786c3bf7e9d55994f4e0b4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="logging-in-the-script-task"></a>Registrar en la tarea Script
  El uso del registro en los paquetes de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] permite registrar información detallada sobre el progreso, los resultados y los problemas de ejecución al registrar eventos predefinidos o mensajes definidos por el usuario para su análisis posterior. La tarea Script puede utilizar el método <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> del objeto **Dts** para registrar datos definidos por el usuario. Si el registro está habilitado y se selecciona el evento **ScriptTaskLogEntry** para el registro en la pestaña **Detalles** del cuadro de diálogo **Configurar registros de SSIS**, una sola llamada al método <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> almacena la información de eventos en todos los proveedores de registro configurados para la tarea.  
  
> [!NOTE]  
>  Si bien puede realizar registros directamente desde la tarea Script, puede que le interese implementar los eventos en lugar de registrarlos. Al utilizar eventos, no solamente puede habilitar el registro de mensajes de evento, sino que también puede responder al evento con controladores de eventos predeterminados o definidos por el usuario.  
  
 Para obtener más información sobre el registro, vea [Registro de Integration Services &#40;SSIS&#41;](../../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="logging-example"></a>Ejemplo de registro  
 En el ejemplo siguiente se muestra el registro de la tarea Script mediante el registro de un valor que representa el número de filas procesadas.  
  
```vb  
Public Sub Main()  
  
    Dim rowsProcessed As Integer = 100  
    Dim emptyBytes(0) As Byte  
  
    Try  
        Dts.Log("Rows processed: " & rowsProcessed.ToString, _  
            0, _  
            emptyBytes)  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        'An error occurred.  
        Dts.Events.FireError(0, "Script Task Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
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
            //  
            int rowsProcessed = 100;  
            byte[] emptyBytes = new byte[0];  
  
            try  
            {  
                Dts.Log("Rows processed: " + rowsProcessed.ToString(), 0, emptyBytes);  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                //An error occurred.  
                Dts.Events.FireError(0, "Script Task Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
        }  
```  
  
 }  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Entrada de blog [Logging custom events for Integration Services tasks (Registro de eventos personalizados para tareas de Integration Services)](http://go.microsoft.com/fwlink/?LinkId=165644) en dougbert.com.  
  
## <a name="see-also"></a>Ver también  
 [Registro de Integration Services &#40;SSIS&#41;](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  

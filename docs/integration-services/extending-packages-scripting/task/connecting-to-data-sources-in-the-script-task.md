---
title: "Conectarse a orígenes de datos de la tarea Script | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
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
- connections [Integration Services], scripts
- Integration Services packages, connections
- connection managers [Integration Services], scripts
- scripts [Integration Services], connections
- SSIS packages, connections
- packages [Integration Services], connections
- Script task [Integration Services], connections
- Connections property
- SQL Server Integration Services packages, connections
- SSIS Script task, connections
ms.assetid: 9c008380-715b-455b-9da7-22572d67c388
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 825ff059476614085a338dd9c568031885bed64b
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="connecting-to-data-sources-in-the-script-task"></a>Conectarse a orígenes de datos de la tarea Script
  Los administradores de conexiones proporcionan acceso a los orígenes de datos configurados en el paquete. Para más información, vea [Conexiones de Integration Services &#40;SSIS&#41;](../../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
 La tarea Script puede tener acceso a estos administradores de conexión a través de la <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> propiedad de la **Dts** objeto. Todos los administradores de conexión de la colección <xref:Microsoft.SqlServer.Dts.Runtime.Connections> almacenan información sobre cómo conectarse al origen de datos subyacente.  
  
 Cuando llama al método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> de un administrador de conexiones, el administrador de conexiones se conecta al origen de datos, si aún no está conectado, y devuelve la información de conexión o la conexión adecuada para que la utilice en el código de la tarea Script.  
  
> [!NOTE]  
>  Debe conocer el tipo de conexión devuelto por el Administrador de conexiones antes de llamar a **AcquireConnection**. Dado que la tarea Script tiene **Option Strict** habilitado, debe convertir la conexión, que se devuelve como tipo **objeto**, para el tipo de conexión adecuado antes de utilizarla.  
  
 Puede utilizar el método <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Contains%2A> de la colección <xref:Microsoft.SqlServer.Dts.Runtime.Connections> devuelto por la propiedad <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> para buscar una conexión existente antes de utilizar la conexión en el código.  
  
> [!IMPORTANT]  
>  No se puede llamar al método AcquireConnection administradores de conexión que devuelven objetos no administrados, como el Administrador de conexiones OLE DB y el Administrador de conexiones de Excel, en el código administrado de una tarea de secuencia de comandos. Sin embargo, puede leer la propiedad ConnectionString de estos administradores de conexión y conectarse al origen de datos directamente en el código mediante el uso de la cadena de conexión con un **OledbConnection** desde el **System.Data.OleDb** espacio de nombres.  
>   
>  Si debe llamar a la llamada del método AcquireConnection de una conexión de administrador que devuelve un objeto no administrado, use un [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] Administrador de conexiones. Al configurar el administrador de conexiones [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] para utilizar un proveedor OLE DB, se conecta mediante el proveedor de datos de [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] para OLE DB. En este caso, se devuelve el método AcquireConnection un **System.Data.OleDb.OleDbConnection** en lugar de un objeto no administrado. Para configurar un [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] Administrador de conexiones para su uso con un origen de datos de Excel, seleccione la [!INCLUDE[msCoName](../../../includes/msconame-md.md)] proveedor OLE DB para Jet, especifique un archivo de Excel y escriba `Excel 8.0` (para Excel 97 y posterior) como el valor de **propiedades extendidas** en el **todos los** página de la **Connection Manager** cuadro de diálogo.  
  
## <a name="connections-example"></a>Ejemplo de conexiones  
 En el ejemplo siguiente se muestra cómo obtener acceso a los administradores de conexión desde dentro de la tarea Script. El ejemplo se supone que ha creado y configurado un [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] Administrador de conexiones denominado **Test ADO.NET Connection** y un administrador de conexión de archivos planos denominado **Test Flat File Connection**. Tenga en cuenta que la [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] Administrador de conexiones devuelve una **SqlConnection** objeto que se puede utilizar inmediatamente para conectarse al origen de datos. El administrador de conexiones de archivos planos, por otro lado, devuelve solamente una cadena que contiene la ruta de acceso y el nombre de archivo. Debe usar los métodos de la **System.IO** espacio de nombres para abrirla y trabajar con el archivo sin formato.  
  
```vb  
Public Sub Main()  
  
    Dim myADONETConnection As SqlClient.SqlConnection  
    myADONETConnection = _  
        DirectCast(Dts.Connections("Test ADO.NET Connection").AcquireConnection(Dts.Transaction), _  
        SqlClient.SqlConnection)  
    MsgBox(myADONETConnection.ConnectionString, _  
        MsgBoxStyle.Information, "ADO.NET Connection")  
  
    Dim myFlatFileConnection As String  
    myFlatFileConnection = _  
        DirectCast(Dts.Connections("Test Flat File Connection").AcquireConnection(Dts.Transaction), _  
        String)  
    MsgBox(myFlatFileConnection, MsgBoxStyle.Information, "Flat File Connection")  
  
    Dts.TaskResult = ScriptResults.Success  
  
End Sub  
```  
  
```csharp  
using System;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Windows.Forms;  
  
public class ScriptMain  
{  
  
        public void Main()  
        {  
            SqlConnection myADONETConnection = new SqlConnection();  
            myADONETConnection = (SqlConnection)(Dts.Connections["Test ADO.NET Connection"].AcquireConnection(Dts.Transaction)as SqlConnection);  
            MessageBox.Show(myADONETConnection.ConnectionString, "ADO.NET Connection");  
  
            string myFlatFileConnection;  
            myFlatFileConnection = (string)(Dts.Connections["Test Flat File Connection"].AcquireConnection(Dts.Transaction) as String);  
            MessageBox.Show(myFlatFileConnection, "Flat File Connection");  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
}  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Integration Services &#40; SSIS &#41; Conexiones](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Crear administradores de conexión](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  


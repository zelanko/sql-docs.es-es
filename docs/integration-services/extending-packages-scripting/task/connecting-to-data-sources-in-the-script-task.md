---
title: Conectarse a orígenes de datos de la tarea Script | Microsoft Docs
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9f042d3039902a9e061feabf9567a5fbad250562
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2018
ms.locfileid: "51641902"
---
# <a name="connecting-to-data-sources-in-the-script-task"></a>Conectarse a orígenes de datos de la tarea Script
  Los administradores de conexiones proporcionan acceso a los orígenes de datos configurados en el paquete. Para más información, vea [Conexiones de Integration Services &#40;SSIS&#41;](../../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
 La tarea Script tiene acceso a estos administradores de conexiones a través de la propiedad <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> del objeto**Dts**. Todos los administradores de conexión de la colección <xref:Microsoft.SqlServer.Dts.Runtime.Connections> almacenan información sobre cómo conectarse al origen de datos subyacente.  
  
 Cuando llama al método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> de un administrador de conexiones, el administrador de conexiones se conecta al origen de datos, si aún no está conectado, y devuelve la información de conexión o la conexión adecuada para que la utilice en el código de la tarea Script.  
  
> [!NOTE]  
>  Debe conocer el tipo de conexión que devuelve el administrador de conexiones antes de llamar a **AcquireConnection**. Dado que la tarea Script tiene habilitado **Option Strict**, debe convertir la conexión, que se devuelve como tipo **Object**, al tipo de conexión adecuado antes de poder utilizarlo.  
  
 Puede utilizar el método <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Contains%2A> de la colección <xref:Microsoft.SqlServer.Dts.Runtime.Connections> devuelto por la propiedad <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> para buscar una conexión existente antes de utilizar la conexión en el código.  
  
> [!IMPORTANT]  
>  No puede llamar al método AcquireConnection de los administradores de conexiones que devuelvan objetos no administrados, como el administrador de conexiones OLE DB y el administrador de conexiones Excel, en el código administrado de una tarea Script. Sin embargo, puede leer la propiedad ConnectionString de estos administradores de conexiones y conectarse directamente al origen de datos en el código utilizando la cadena de conexión con **OledbConnection** del espacio de nombres **System.Data.OleDb**.  
>   
>  Si debe llamar al método AcquireConnection de un administrador de conexiones que devuelve un objeto no administrado, utilice un administrador de conexiones [!INCLUDE[vstecado](../../../includes/vstecado-md.md)]. Al configurar el administrador de conexiones [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] para utilizar un proveedor OLE DB, se conecta mediante el proveedor de datos de [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] para OLE DB. En este caso, el método AcquireConnection devuelve **System.Data.OleDb.OleDbConnection**, en lugar de un objeto no administrado. Para configurar un administrador de conexiones [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] para su uso con un origen de datos Excel, seleccione el proveedor OLE DB de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] para Jet, especifique un archivo de Excel y, a continuación, escriba `Excel 8.0` (para Excel 97 y posterior) como el valor de **Propiedades extendidas** en la página **Todas** del cuadro de diálogo **Administrador de conexiones**.  
  
## <a name="connections-example"></a>Ejemplo de conexiones  
 En el ejemplo siguiente se muestra cómo obtener acceso a los administradores de conexión desde dentro de la tarea Script. En el ejemplo se supone que ha creado y configurado un administrador de conexiones [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] denominado **Test ADO.NET Connection** y un administrador de conexiones de archivos planos denominado **Test Flat File Connection**. Observe que el administrador de conexiones [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] devuelve un objeto **SqlConnection** que puede utilizar inmediatamente para conectarse al origen de datos. El administrador de conexiones de archivos planos, por otro lado, devuelve solamente una cadena que contiene la ruta de acceso y el nombre de archivo. Debe utilizar los métodos del espacio de nombres **System.IO** para abrir el archivo plano y trabajar con este.  
  
```vb  
    Public Sub Main()

        Dim myADONETConnection As SqlClient.SqlConnection =
            DirectCast(Dts.Connections("Test ADO.NET Connection").AcquireConnection(Dts.Transaction),
                SqlClient.SqlConnection)
        MsgBox(myADONETConnection.ConnectionString,
            MsgBoxStyle.Information, "ADO.NET Connection")

        Dim myFlatFileConnection As String =
            DirectCast(Dts.Connections("Test Flat File Connection").AcquireConnection(Dts.Transaction),
                String)
        MsgBox(myFlatFileConnection, MsgBoxStyle.Information, "Flat File Connection")

        Dts.TaskResult = ScriptResults.Success

    End Sub
```  
  
```csharp  
        public void Main()
        {
            SqlConnection myADONETConnection = 
                Dts.Connections["Test ADO.NET Connection"].AcquireConnection(Dts.Transaction)
                as SqlConnection;
            MessageBox.Show(myADONETConnection.ConnectionString, "ADO.NET Connection");

            string myFlatFileConnection = 
                Dts.Connections["Test Flat File Connection"].AcquireConnection(Dts.Transaction) 
                as string;
            MessageBox.Show(myFlatFileConnection, "Flat File Connection");

            Dts.TaskResult = (int)ScriptResults.Success;
        }
```  
  
## <a name="see-also"></a>Ver también  
 [Conexiones de Integration Services &#40;SSIS&#41;](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Crear administradores de conexiones](https://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  

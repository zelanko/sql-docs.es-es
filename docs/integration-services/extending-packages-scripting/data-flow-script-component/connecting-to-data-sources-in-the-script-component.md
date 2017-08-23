---
title: "Conectarse a orígenes de datos en el componente de Script | Documentos de Microsoft"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], connecting to data sources
ms.assetid: 96de63ab-ff48-4e7e-89e0-ffd6a89c63b6
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e2accca553f1bd9c536076fd0bbcebbff0ff2c42
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="connecting-to-data-sources-in-the-script-component"></a>Conectarse a orígenes de datos del componente de script
  Un administrador de conexiones es una unidad práctica que encapsula y almacena la información necesaria para conectarse a un origen de datos de un tipo determinado. Para más información, vea [Conexiones de Integration Services &#40;SSIS&#41;](../../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
 Hacer que los administradores de conexión existentes disponibles para acceso de parte del script personalizado en el componente de origen o destino haciendo clic en el **agregar** y **quitar** botones en la **administradores de conexión** página de la **Editor de transformación Script**. Sin embargo, debe escribir su propio código personalizado para cargar o guardar los datos y posiblemente para abrir y cerrar la conexión al origen de datos. Para obtener más información sobre la **administradores de conexión** página de la **Editor de transformación Script**, consulte [configurar el componente de Script en el Editor de componentes de secuencia de comandos](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md) y [Editor de transformación Script &#40; Página Administradores de conexión &#41; ](../../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
 El componente de Script crea una **conexiones** clase de colección en el **ComponentWrapper** elemento de proyecto que contiene un descriptor de acceso fuertemente tipado para cada administrador de conexiones que tiene el mismo nombre que el propio administrador de conexiones. Esta colección se expone a través de la **conexiones** propiedad de la **ScriptMain** clase. La propiedad de descriptor de acceso devuelve una referencia al administrador de conexiones como una instancia de <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100>. Por ejemplo, si ha agregado un administrador de conexiones denominado `MyADONETConnection` en la página Administradores de conexión del cuadro de diálogo, puede obtener una referencia a dicho administrador en el script agregando el código siguiente:  
  
 `Dim myADONETConnectionManager As IDTSConnectionManager100 = _`  
  
 `Me.Connections.MyADONETConnection`  
  
> [!NOTE]  
>  Debe conocer el tipo de conexión que es devuelto por el Administrador de conexiones antes de llamar a **AcquireConnection**. Dado que la tarea Script tiene **Option Strict** habilitado, debe convertir la conexión, que se devuelve como tipo **objeto**, para el tipo de conexión adecuado antes de utilizarla.  
  
 A continuación, se llama a la **AcquireConnection** método del Administrador de conexión específica para obtener la conexión subyacente o la información necesaria para conectarse al origen de datos. Por ejemplo, puede obtener una referencia a la **System.Data.SqlConnection** ajustada por un administrador de conexiones de ADO.NET mediante el código siguiente:  
  
 `Dim myADOConnection As SqlConnection = _`  
  
 `CType(MyADONETConnectionManager.AcquireConnection(Nothing), SqlConnection)`  
  
 En cambio, la misma llamada a un administrador de conexiones de archivos planos devuelve solamente la ruta de acceso y nombre de archivo del origen de datos de archivo.  
  
 `Dim myFlatFile As String = _`  
  
 `CType(MyFlatFileConnectionManager.AcquireConnection(Nothing), String)`  
  
 A continuación, debe proporcionar esta ruta de acceso y nombre de archivo a un **System.IO.StreamReader** o **Streamwriter** para leer o escribir los datos en el archivo sin formato.  
  
> [!IMPORTANT]  
>  Cuando se escribe código administrado en un componente de Script, no se puede llamar al método AcquireConnection de conexión administradores que devuelven objetos no administrados, como el Administrador de conexiones OLE DB y el Administrador de conexiones de Excel. Sin embargo, puede leer la propiedad ConnectionString de estos administradores de conexión y conectarse al origen de datos directamente en el código mediante el uso de la cadena de conexión de un OLEDB **conexión** desde el **System.Data.OleDb** espacio de nombres.  
>   
>  Si tiene que llamar al método AcquireConnection de un administrador de conexiones que devuelve un objeto no administrado, utilice un administrador de conexiones de ADO.NET. Al configurar el administrador de conexiones ADO.NET para utilizar un proveedor OLE DB, se conecta mediante el proveedor de datos de .NET Framework para OLE DB. En este caso, se devuelve el método AcquireConnection un **System.Data.OleDb.OleDbConnection** en lugar de un objeto no administrado. Para configurar un administrador de conexiones de ADO.NET para su uso con un origen de datos de Excel, seleccione el proveedor Microsoft OLE DB para Jet, especifique un libro de Excel y, a continuación, escriba `Excel 8.0` (para Excel 97 y posterior) como el valor de **propiedades extendidas** en el **todos los** página de la **Connection Manager** cuadro de diálogo.  
  
 Para obtener más información acerca de cómo se utilizan los administradores de conexión con el componente de script, consulte [crear un origen con el componente de Script](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md) y [crear un destino con el componente de Script](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md).  
  
## <a name="see-also"></a>Vea también  
 [Integration Services &#40; SSIS &#41; Conexiones](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Crear administradores de conexión](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  

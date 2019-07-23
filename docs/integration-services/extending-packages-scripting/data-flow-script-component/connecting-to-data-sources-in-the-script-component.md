---
title: Conectarse a orígenes de datos del componente de script | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], connecting to data sources
ms.assetid: 96de63ab-ff48-4e7e-89e0-ffd6a89c63b6
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 5ce23e61be7264ecb958604681cd7271446540eb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104015"
---
# <a name="connecting-to-data-sources-in-the-script-component"></a>Conectarse a orígenes de datos del componente de script

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Un administrador de conexiones es una unidad práctica que encapsula y almacena la información necesaria para conectarse a un origen de datos de un tipo determinado. Para más información, vea [Conexiones de Integration Services &#40;SSIS&#41;](../../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
 Para hacer que los administradores de conexiones existentes estén disponibles para el acceso por parte del script personalizado del componente de origen o de destino, haga clic en los botones **Agregar** y **Quitar** de la página **Administradores de conexiones** del **Editor de transformación Script**. Sin embargo, debe escribir su propio código personalizado para cargar o guardar los datos y posiblemente para abrir y cerrar la conexión al origen de datos. Para obtener más información acerca de la página **Administradores de conexiones** del **Editor de transformación Script**, vea [Configurar el componente de script en el editor de componentes de script](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md) y [Editor de transformación Script &#40;página Administradores de conexiones&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
 El componente de script crea una clase de colección **Connections** en el elemento de proyecto **ComponentWrapper** que contiene un descriptor de acceso fuertemente tipado para cada administrador de conexiones que tiene el mismo nombre que el propio administrador de conexiones. Esta colección se expone mediante la propiedad **Connections** de la clase **ScriptMain**. La propiedad de descriptor de acceso devuelve una referencia al administrador de conexiones como una instancia de <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100>. Por ejemplo, si ha agregado un administrador de conexiones denominado `MyADONETConnection` en la página Administradores de conexión del cuadro de diálogo, puede obtener una referencia a dicho administrador en el script agregando el código siguiente:  
  
 `Dim myADONETConnectionManager As IDTSConnectionManager100 = _`  
  
 `Me.Connections.MyADONETConnection`  
  
> [!NOTE]  
>  Debe conocer el tipo de conexión que el administrador de conexiones devuelve antes de llamar a **AcquireConnection**. Dado que la tarea Script tiene habilitado **Option Strict**, debe convertir la conexión, que se devuelve como tipo **Object**, al tipo de conexión adecuado antes de poder utilizarlo.  
  
 A continuación, puede llamar al método **AcquireConnection** del administrador de conexiones concreto para obtener la conexión subyacente o la información necesaria para conectarse al origen de datos. Por ejemplo, puede obtener una referencia al objeto **System.Data.SqlConnection** ajustado por un administrador de conexiones ADO.NET utilizando el código siguiente:  
  
 `Dim myADOConnection As SqlConnection = _`  
  
 `CType(MyADONETConnectionManager.AcquireConnection(Nothing), SqlConnection)`  
  
 En cambio, la misma llamada a un administrador de conexiones de archivos planos devuelve solamente la ruta de acceso y nombre de archivo del origen de datos de archivo.  
  
 `Dim myFlatFile As String = _`  
  
 `CType(MyFlatFileConnectionManager.AcquireConnection(Nothing), String)`  
  
 A continuación, debe proporcionar esta ruta de acceso y nombre de archivo a **System.IO.StreamReader** o **Streamwriter** para leer o escribir los datos en el archivo plano.  
  
> [!IMPORTANT]  
>  Al escribir el código administrado en un componente de script, no puede llamar al método AcquireConnection de los administradores de conexiones que devuelven objetos no administrados, como el administrador de conexiones de OLE DB y el administrador de conexiones de Excel. Sin embargo, puede leer la propiedad ConnectionString de estos administradores de conexiones y conectarse directamente al origen de datos en el código utilizando la cadena de conexión de una **conexión** OLEDB del espacio de nombres **System.Data.OleDb**.  
>   
>  Si tiene que llamar al método AcquireConnection de un administrador de conexiones que devuelve un objeto no administrado, utilice un administrador de conexiones ADO.NET. Al configurar el administrador de conexiones ADO.NET para utilizar un proveedor OLE DB, se conecta mediante el proveedor de datos de .NET Framework para OLE DB. En este caso, el método AcquireConnection devuelve **System.Data.OleDb.OleDbConnection**, en lugar de un objeto no administrado. Para configurar un administrador de conexiones ADO.NET para su uso con un origen de datos de Excel, seleccione el proveedor OLE DB de Microsoft para Jet, especifique un libro de Excel y, a continuación, escriba `Excel 8.0` (para Excel 97 y posterior) como el valor de **Propiedades extendidas** en la página **Todas** del cuadro de diálogo **Administrador de conexiones**.  
  
 Para obtener más información acerca de cómo se utilizan los administradores de conexiones con el componente de script, consulte [Crear un origen con el componente de script](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md) y [Crear un destino con el componente de script](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md).  
  
## <a name="see-also"></a>Consulte también  
 [Conexiones de Integration Services &#40;SSIS&#41;](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Crear administradores de conexiones](https://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  

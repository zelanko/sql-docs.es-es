---
title: Descripción del modelo de objetos del componente de script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], object model
ms.assetid: 2a0aae82-39cc-4423-b09a-72d2f61033bd
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 855278c35de37f2b02e1bb7b194e174c66c643d2
ms.sourcegitcommit: ef78cc196329a10fc5c731556afceaac5fd4cb13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2018
ms.locfileid: "49460670"
---
# <a name="understanding-the-script-component-object-model"></a>Descripción del modelo de objetos del componente de script
  Como se describe en [codificar y depurar el componente de Script] (.. / extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md, el proyecto de componente de Script contiene tres elementos de proyecto:  
  
1.  El elemento `ScriptMain`, que contiene la clase `ScriptMain` donde se escribe el código. La clase `ScriptMain` hereda de la clase `UserComponent`.  
  
2.  El elemento `ComponentWrapper`, que contiene la clase `UserComponent`, una instancia de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> que contiene los métodos y propiedades que utilizará para procesar los datos e interactuar con el paquete. El elemento `ComponentWrapper` también contiene las clases de colección `Connections` y `Variables`.  
  
3.  El elemento `BufferWrapper`, que contiene clases que hereda de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> para cada entrada y salida, así como propiedades con tipo para cada columna.  
  
 Al escribir el código en el elemento `ScriptMain`, utiliza los objetos, métodos y propiedades que se explican en este tema. Cada uno de los componentes no utilizará todos los métodos que se enumeran aquí; sin embargo, cuando se utilizan, lo hacen en la secuencia mostrada.  
  
 La clase base <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> no contiene ningún código de la implementación para los métodos descritos en este tema. Por tanto no es necesario, aunque tampoco es perjudicial, que agregue una llamada a la implementación de la clase base en su propia implementación del método.  
  
 Para obtener información acerca de cómo usar los métodos y propiedades de estas clases en un tipo determinado del componente de script, vea la sección [Additional Script Component Examples](../../extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md) (Ejemplos de componente de script adicionales). Los temas de ejemplo también contienen ejemplos de código completos.  
  
## <a name="acquireconnections-method"></a>Método AcquireConnections  
 Generalmente, los orígenes y destinos deben conectarse a un origen de datos externo. Invalide el método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A> de la clase base <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> para recuperar la conexión o la información de conexión del administrador de conexiones adecuado.  
  
 En el ejemplo siguiente se devuelve `System.Data.SqlClient.SqlConnection` de un administrador de conexiones ADO.NET.  
  
```vb  
Dim connMgr As IDTSConnectionManager100  
Dim sqlConn As SqlConnection  
  
Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
    connMgr = Me.Connections.MyADONETConnection  
    sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
End Sub  
```  
  
 En el ejemplo siguiente se devuelve una ruta de acceso completa y el nombre de archivo de un administrador de conexiones de archivos planos y, a continuación, se abre el archivo mediante `System.IO.StreamReader`.  
  
```vb  
Private textReader As StreamReader  
Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
    Dim connMgr As IDTSConnectionManager100 = _  
        Me.Connections.MyFlatFileSrcConnectionManager  
    Dim exportedAddressFile As String = _  
        CType(connMgr.AcquireConnection(Nothing), String)  
    textReader = New StreamReader(exportedAddressFile)  
  
End Sub  
```  
  
## <a name="preexecute-method"></a>Método PreExecute  
 Invalide el método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PreExecute%2A> de la clase base <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> siempre que tenga que realizar el procesamiento una sola vez antes de iniciar el procesamiento de las filas de datos. Por ejemplo, en un destino, es posible que desee configurar el comando con parámetros que utilizará el destino para insertar cada fila de datos en el origen de datos.  
  
```vb  
    Dim sqlConn As SqlConnection  
    Dim sqlCmd As SqlCommand  
    Dim sqlParam As SqlParameter  
...  
    Public Overrides Sub PreExecute()  
  
        sqlCmd = New SqlCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
            "VALUES(@addressid, @city)", sqlConn)  
        sqlParam = New SqlParameter("@addressid", SqlDbType.Int)  
        sqlCmd.Parameters.Add(sqlParam)  
        sqlParam = New SqlParameter("@city", SqlDbType.NVarChar, 30)  
        sqlCmd.Parameters.Add(sqlParam)  
  
    End Sub  
```  
  
```csharp  
SqlConnection sqlConn;   
SqlCommand sqlCmd;   
SqlParameter sqlParam;   
  
public override void PreExecute()   
{   
  
    sqlCmd = new SqlCommand("INSERT INTO Person.Address2(AddressID, City) " + "VALUES(@addressid, @city)", sqlConn);   
    sqlParam = new SqlParameter("@addressid", SqlDbType.Int);   
    sqlCmd.Parameters.Add(sqlParam);   
    sqlParam = new SqlParameter("@city", SqlDbType.NVarChar, 30);   
    sqlCmd.Parameters.Add(sqlParam);   
  
}  
```  
  
## <a name="processing-inputs-and-outputs"></a>Procesar entradas y salidas  
  
### <a name="processing-inputs"></a>Procesar entradas  
 Los componentes de script que se configuran como transformaciones o destinos tienen una entrada.  
  
#### <a name="what-the-bufferwrapper-project-item-provides"></a>Qué proporciona el elemento de proyecto BufferWrapper  
 Para cada entrada que ha configurado, el elemento de proyecto `BufferWrapper` contiene una clase que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> y tiene el mismo nombre que la entrada. Cada clase de búfer de entrada contiene las siguientes propiedades, funciones y métodos:  
  
-   Propiedades de descriptor de acceso con nombre y tipo para cada columna de entrada seleccionada. Estas propiedades son de solo lectura o de lectura y escritura, dependiendo del **Tipo de uso** especificado para la columna en la página **Columnas de entrada** del **Editor de transformación Script**.  
  
-   Una propiedad **\<column>_IsNull** para cada columna de entrada seleccionada. Esta propiedad también es de solo lectura o de lectura y escritura, dependiendo del **Tipo de uso** especificado para la columna.  
  
-   Un método **DirectRowTo\<outputbuffer>** para cada salida configurada. Utilizará estos métodos al filtrar las filas a una de varias salidas en el mismo `ExclusionGroup`.  
  
-   Una función `NextRow` para obtener la siguiente fila de entrada y una función `EndOfRowset` para determinar si se ha procesado el último búfer de datos. Normalmente no necesita estas funciones al utilizar los métodos de procesamiento de entrada implementados en la clase base `UserComponent`. En la sección siguiente se proporciona más información sobre la clase base `UserComponent`.  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>Qué proporciona el elemento de proyecto ComponentWrapper  
 El elemento de proyecto ComponentWrapper contiene una clase denominada `UserComponent` que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>. La clase `ScriptMain` donde escribe el código personalizado deriva a su vez de `UserComponent`. La clase `UserComponent` contiene los siguientes métodos:  
  
-   Una implementación invalidada del método `ProcessInput`. Éste es el método al que el motor de flujo de datos llama en tiempo de ejecución después del método `PreExecute` y al que se puede llamar varias veces. `ProcessInput` entrega el procesamiento para la  **\<inputbuffer > _ProcessInput** método. A continuación, el método `ProcessInput` comprueba el fin del búfer de entrada y, si se ha alcanzado, llama al método reemplazable `FinishOutputs` y al método privado `MarkOutputsAsFinished`. A continuación, el método `MarkOutputsAsFinished` llama a `SetEndOfRowset` en el último búfer de salida.  
  
-   Una implementación reemplazable del método **\<inputbuffer>_ProcessInput**. Esta implementación predeterminada, simplemente, recorre en bucle cada fila de entrada y llama a **\<inputbuffer>_ProcessInputRow**.  
  
-   Una implementación reemplazable del método **\<inputbuffer>_ProcessInputRow**. La implementación predeterminada está vacía. Éste es el método que normalmente invalidará para escribir el código personalizado de procesamiento de datos.  
  
#### <a name="what-your-custom-code-should-do"></a>Qué debe hacer el código personalizado  
 Puede utilizar los métodos siguientes para procesar la entrada en la clase `ScriptMain`:  
  
-   Invalide **\<inputbuffer>_ProcessInputRow** para procesar los datos de cada fila de entrada cuando el código pase por ellos.  
  
-   Invalide **\<inputbuffer>_ProcessInput** solamente si es necesaria alguna acción adicional mientras se recorren en bucle las filas de entrada. (Por ejemplo, si tiene que comprobar `EndOfRowset` para realizar alguna otra acción una vez procesadas todas las filas.) Llame a **\<inputbuffer>_ProcessInputRow** para realizar el procesamiento de filas.  
  
-   Invalide `FinishOutputs` si es necesaria alguna acción adicional en las salidas antes de cerrarlas.  
  
 El método `ProcessInput` garantiza que las llamadas a estos métodos se realizan en el momento adecuado.  
  
### <a name="processing-outputs"></a>Procesar salidas  
 Los componentes de script configurados como orígenes o transformaciones tienen una o más salidas.  
  
#### <a name="what-the-bufferwrapper-project-item-provides"></a>Qué proporciona el elemento de proyecto BufferWrapper  
 Para cada salida que ha configurado, el elemento de proyecto BufferWrapper contiene una clase que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> y tiene el mismo nombre que la salida. Cada clase de búfer de entrada contiene las siguientes propiedades y métodos:  
  
-   Propiedades de descriptor de acceso con nombre y tipo de solo escritura para cada columna de salida.  
  
-   Solo escritura  **\<columna > _IsNull** propiedad para cada columna de salida seleccionada que puede usar para establecer el valor de columna en `null`.  
  
-   Un método `AddRow` para agregar una nueva fila vacía al búfer de salida.  
  
-   Un método `SetEndOfRowset` para permitir que el motor de flujo de datos sepa que no se esperan más búferes de datos. También existe una función `EndOfRowset` para determinar si el búfer actual es el último búfer de datos. Por lo general no necesita estas funciones cuando se usa la entrada de procesamiento de los métodos implementados en el `UserComponent` clase base.  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>Qué proporciona el elemento de proyecto ComponentWrapper  
 El elemento de proyecto ComponentWrapper contiene una clase denominada `UserComponent` que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>. La clase `ScriptMain` donde escribe el código personalizado deriva a su vez de `UserComponent`. La clase `UserComponent` contiene los siguientes métodos:  
  
-   Una implementación invalidada del método `PrimeOutput`. El motor de flujo de datos llama a este método antes de `ProcessInput` en tiempo de ejecución y solamente lo llama una vez. `PrimeOutput` entrega el procesamiento al método `CreateNewOutputRows`. A continuación, si el componente es un origen (es decir, el componente no tiene ninguna entrada), `PrimeOutput` llama al método reemplazable `FinishOutputs` y al método privado `MarkOutputsAsFinished`. El método `MarkOutputsAsFinished` llama a `SetEndOfRowset` en el último búfer de salida.  
  
-   Una implementación reemplazable del método `CreateNewOutputRows`. La implementación predeterminada está vacía. Éste es el método que normalmente invalidará para escribir el código personalizado de procesamiento de datos.  
  
#### <a name="what-your-custom-code-should-do"></a>Qué debe hacer el código personalizado  
 Puede utilizar los métodos siguientes para procesar las salidas en la clase `ScriptMain`:  
  
-   Invalide `CreateNewOutputRows` solamente si puede agregar y rellenar las filas de salida antes de procesar las filas de entrada. Por ejemplo, puede utilizar `CreateNewOutputRows` en un origen, pero en una transformación con salidas asincrónicas debe llamar a `AddRow` durante o después del procesamiento de los datos de entrada.  
  
-   Invalide `FinishOutputs` si es necesaria alguna acción adicional en las salidas antes de cerrarlas.  
  
 El método `PrimeOutput` garantiza que las llamadas a estos métodos se realizan en el momento adecuado.  
  
## <a name="postexecute-method"></a>Método PostExecute  
 Invalide el método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PostExecute%2A> de la clase base <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> cada vez que cuente con procesamiento que se debe realizar solamente una vez después de procesar las filas de datos. Por ejemplo, en un origen, puede cerrar la clase `System.Data.SqlClient.SqlDataReader` que ha utilizado para cargar datos en el flujo de datos.  
  
> [!IMPORTANT]  
>  La colección de `ReadWriteVariables` solamente está disponible en el método `PostExecute`. Por consiguiente no puede incrementar directamente el valor de una variable de paquete cuando procesa cada fila de datos. En su lugar, incremente el valor de una variable local y establezca el valor de la variable de paquete en el valor de la variable local en el `PostExecute` método después de todos los datos se ha procesado.  
  
## <a name="releaseconnections-method"></a>Método ReleaseConnections  
 Generalmente, los orígenes y destinos deben conectarse a un origen de datos externo. Invalide el método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReleaseConnections%2A> de la clase base <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> para cerrar y liberar la conexión abierta previamente en el método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A>.  
  
```vb  
    Dim connMgr As IDTSConnectionManager100  
...  
    Public Overrides Sub ReleaseConnections()  
  
        connMgr.ReleaseConnection(sqlConn)  
  
    End Sub  
```  
  
```csharp  
IDTSConnectionManager100 connMgr;  
  
public override void ReleaseConnections()  
{  
  
    connMgr.ReleaseConnection(sqlConn);  
  
}  
```  
  
![Icono de Integration Services (pequeño)](../../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Vea también  
 [Configuring the Script Component in the Script Component Editor](configuring-the-script-component-in-the-script-component-editor.md)  (Configurar el componente de script en el editor de componentes de script)  
 [Codificar y depurar el componente de Script] (.. /Extending-Packages-scripting/Data-Flow-script-Component/Coding-and-Debugging-the-Script-Component.MD  
  
  

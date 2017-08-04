---
title: "Descripción del modelo de objetos de componentes de Script | Documentos de Microsoft"
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
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], object model
ms.assetid: 2a0aae82-39cc-4423-b09a-72d2f61033bd
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 09de00344fe94087b6287b07c4b1ffe933d27b7c
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="understanding-the-script-component-object-model"></a>Descripción del modelo de objetos del componente de script
  Como se describe en [codificar y depurar el componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md), el proyecto de componente de Script contiene tres elementos de proyecto:  
  
1.  El **ScriptMain** elemento, que contiene el **ScriptMain** en el que se escribe el código de clase. El **ScriptMain** clase hereda de la **UserComponent** clase.  
  
2.  El **ComponentWrapper** elemento, que contiene el **UserComponent** de la clase, una instancia de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> que contiene los métodos y propiedades que se va a usar para procesar los datos e interactuar con el paquete. El **ComponentWrapper** elemento también contiene **conexiones** y **Variables** clases de colección.  
  
3.  El **BufferWrapper** elemento, que contiene clases que hereda de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> para cada propiedades de entrada y salida y con tipo para cada columna.  
  
 Al escribir el código en el **ScriptMain** elemento, utilizará los objetos, métodos y propiedades que se analizan en este tema. Cada uno de los componentes no utilizará todos los métodos que se enumeran aquí; sin embargo, cuando se utilizan, lo hacen en la secuencia mostrada.  
  
 La clase base <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> no contiene ningún código de la implementación para los métodos descritos en este tema. Por tanto no es necesario, aunque tampoco es perjudicial, que agregue una llamada a la implementación de la clase base en su propia implementación del método.  
  
 Para obtener información sobre cómo usar los métodos y propiedades de estas clases en un determinado tipo de componente de Script, vea la sección [Additional Script Component Examples](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md). Los temas de ejemplo también contienen ejemplos de código completos.  
  
## <a name="acquireconnections-method"></a>Método AcquireConnections  
 Generalmente, los orígenes y destinos deben conectarse a un origen de datos externo. Invalide el método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A> de la clase base <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> para recuperar la conexión o la información de conexión del administrador de conexiones adecuado.  
  
 En el ejemplo siguiente se devuelve una **System.Data.SqlClient.SqlConnection** desde un administrador de conexiones de ADO.NET.  
  
```vb  
Dim connMgr As IDTSConnectionManager100  
Dim sqlConn As SqlConnection  
  
Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
    connMgr = Me.Connections.MyADONETConnection  
    sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
End Sub  
```  
  
 En el ejemplo siguiente se devuelve una ruta de acceso completa y nombre de archivo, un administrador de conexiones de archivo sin formato y, a continuación, se abre el archivo con un **System.IO.StreamReader**.  
  
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
 Para cada entrada que haya configurado, el **BufferWrapper** elemento de proyecto contiene una clase que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> y tiene el mismo nombre que la entrada. Cada clase de búfer de entrada contiene las siguientes propiedades, funciones y métodos:  
  
-   Propiedades de descriptor de acceso con nombre y tipo para cada columna de entrada seleccionada. Estas propiedades son de solo lectura o lectura/escritura según el **tipo de uso** especificado para la columna en la **columnas de entrada** página de la **Editor de transformación Script**.  
  
-   A ** \<columna > _IsNull** columna de propiedades para cada seleccionado de entrada. Esta propiedad también es de solo lectura o lectura/escritura según el **tipo de uso** especificada para la columna.  
  
-   A **DirectRowTo\<outputbuffer >** método para cada salida configurada. Utilizará estos métodos al filtrar las filas a una de varias salidas en la misma **ExclusionGroup**.  
  
-   A **NextRow** función para obtener la siguiente fila de entrada y un **EndOfRowset** función para determinar si se ha procesado el último búfer de datos. Normalmente no necesita estas funciones cuando utiliza el procesamiento de los métodos implementados en una entrada del **UserComponent** clase base. La siguiente sección proporciona más información sobre la **UserComponent** clase base.  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>Qué proporciona el elemento de proyecto ComponentWrapper  
 El elemento de proyecto ComponentWrapper contiene una clase denominada **UserComponent** que se deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>. El **ScriptMain** clase en la que escribe el código personalizado a su vez deriva de **UserComponent**. El **UserComponent** clase contiene los métodos siguientes:  
  
-   Una implementación invalidada de la **ProcessInput** método. Este es el método que el flujo de datos motor llama en tiempo de ejecución después de la **PreExecute** método y se pueden llamar varias veces. **ProcessInput** entrega el procesamiento para la ** \<inputbuffer > _ProcessInput** método. La **ProcessInput** método comprueba si el final del búfer de entrada y, si se ha alcanzado el final del búfer, llama el reemplazable **FinishOutputs** método y privado **MarkOutputsAsFinished** método. El **MarkOutputsAsFinished** , a continuación, llama a método **SetEndOfRowset** en el último búfer de salida.  
  
-   Una implementación reemplazable de la ** \<inputbuffer > _ProcessInput** método. Esta implementación predeterminada simplemente recorre cada fila de entrada y llama ** \<inputbuffer > _ProcessInputRow**.  
  
-   Una implementación reemplazable de la ** \<inputbuffer > _ProcessInputRow** método. La implementación predeterminada está vacía. Éste es el método que normalmente invalidará para escribir el código personalizado de procesamiento de datos.  
  
#### <a name="what-your-custom-code-should-do"></a>Qué debe hacer el código personalizado  
 Puede usar los métodos siguientes para procesar la entrada en el **ScriptMain** clase:  
  
-   Invalidar ** \<inputbuffer > _ProcessInputRow** para procesar los datos en cada fila de entrada según van pasando por.  
  
-   Invalidar ** \<inputbuffer > _ProcessInput** sólo si tiene que realizar alguna acción adicional mientras en bucle a través de filas de entrada. (Por ejemplo, tendrá que probar **EndOfRowset** para realizar alguna otra acción después de que todos se han procesado filas.) Llame a ** \<inputbuffer > _ProcessInputRow** para realizar el procesamiento de filas.  
  
-   Invalidar **FinishOutputs** si tiene que hacer algo a las salidas antes de que se han cerrado.  
  
 El **ProcessInput** método garantiza que se llama a estos métodos en el momento adecuado.  
  
### <a name="processing-outputs"></a>Procesar salidas  
 Los componentes de script configurados como orígenes o transformaciones tienen una o más salidas.  
  
#### <a name="what-the-bufferwrapper-project-item-provides"></a>Qué proporciona el elemento de proyecto BufferWrapper  
 Para cada salida que ha configurado, el elemento de proyecto BufferWrapper contiene una clase que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> y tiene el mismo nombre que la salida. Cada clase de búfer de entrada contiene las siguientes propiedades y métodos:  
  
-   Propiedades de descriptor de acceso con nombre y tipo de solo escritura para cada columna de salida.  
  
-   De solo escritura ** \<columna > _IsNull** propiedad para cada columna de salida seleccionada que puede usar para establecer el valor de columna en **null**.  
  
-   Un **AddRow** método para agregar una nueva fila vacía al búfer de salida.  
  
-   A **SetEndOfRowset** método para informar al motor de flujo de datos que se esperan que no hay más búferes de datos. También hay un **EndOfRowset** función para determinar si el búfer actual es el último búfer de datos. Por lo general no necesita estas funciones cuando utiliza el procesamiento de los métodos implementados en una entrada del **UserComponent** clase base.  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>Qué proporciona el elemento de proyecto ComponentWrapper  
 El elemento de proyecto ComponentWrapper contiene una clase denominada **UserComponent** que se deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>. El **ScriptMain** clase en la que escribe el código personalizado a su vez deriva de **UserComponent**. El **UserComponent** clase contiene los métodos siguientes:  
  
-   Una implementación invalidada de la **PrimeOutput** método. El motor de flujo de datos llama a este método antes de **ProcessInput** en tiempo de ejecución y solamente lo llama una vez. **PrimeOutput** entrega el procesamiento para la **CreateNewOutputRows** método. A continuación, si el componente es un origen (es decir, el componente no tiene ninguna entrada), **PrimeOutput** llama el reemplazable **FinishOutputs** método y privado **MarkOutputsAsFinished** método. El **MarkOutputsAsFinished** llamadas al método **SetEndOfRowset** en el último búfer de salida.  
  
-   Una implementación reemplazable de la **CreateNewOutputRows** método. La implementación predeterminada está vacía. Éste es el método que normalmente invalidará para escribir el código personalizado de procesamiento de datos.  
  
#### <a name="what-your-custom-code-should-do"></a>Qué debe hacer el código personalizado  
 Puede usar los métodos siguientes para procesar las salidas en el **ScriptMain** clase:  
  
-   Invalidar **CreateNewOutputRows** sólo cuando puede agregar y rellenar las filas de salida antes de procesar filas de entrada. Por ejemplo, puede usar **CreateNewOutputRows** en un origen, pero en una transformación con salidas asincrónicas, debe llamar a **AddRow** durante o después del procesamiento de datos de entrada.  
  
-   Invalidar **FinishOutputs** si tiene que hacer algo a las salidas antes de que se han cerrado.  
  
 El **PrimeOutput** método garantiza que se llama a estos métodos en el momento adecuado.  
  
## <a name="postexecute-method"></a>Método PostExecute  
 Invalide el método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PostExecute%2A> de la clase base <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> cada vez que cuente con procesamiento que se debe realizar solamente una vez después de procesar las filas de datos. Por ejemplo, en un origen, puede cerrar la **System.Data.SqlClient.SqlDataReader** que ha utilizado para cargar datos en el flujo de datos.  
  
> [!IMPORTANT]  
>  La colección de **ReadWriteVariables** sólo está disponible en la **PostExecute** método. Por consiguiente no puede incrementar directamente el valor de una variable de paquete cuando procesa cada fila de datos. En su lugar, aumente el valor de una variable local y establezca el valor de la variable de paquete en el valor de la variable local en el **PostExecute** método después de todos los datos se ha procesado.  
  
## <a name="releaseconnections-method"></a>Método ReleaseConnections  
 Orígenes y destinos normalmente deben conectarse a un origen de datos externo. Invalide el método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReleaseConnections%2A> de la clase base <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> para cerrar y liberar la conexión abierta previamente en el método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A>.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Configurar el componente de Script en el Editor de componentes de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)   
 [Codificar y depurar el componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  

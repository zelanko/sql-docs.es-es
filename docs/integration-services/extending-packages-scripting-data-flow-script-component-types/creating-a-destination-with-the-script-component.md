---
title: Crear un destino con el componente de Script | Documentos de Microsoft
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
- Script component [Integration Services], destination components
- destinations [Integration Services], components
- input columns [Integration Services]
ms.assetid: 214e22e8-7e7d-4876-b690-c138e5721b81
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7680aac73590f92eadd615b9d164967e61877664
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="creating-a-destination-with-the-script-component"></a>Crear un destino con el componente de script
  Los componentes de destino se utilizan en el flujo de datos de un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para guardar datos recibidos de orígenes y transformaciones de nivel superior en un origen de datos. Por lo general, el componente de destino se conecta al origen de datos a través de un administrador de conexiones existente.  
  
 Para obtener información general del componente de Script, consulte [extender el flujo de datos con el componente de Script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
 El componente de script y el código de infraestructura que genera simplifican considerablemente el proceso de desarrollo de un componente de flujo de datos personalizado. Sin embargo, para entender cómo funciona el componente de secuencia de comandos, quizá le resulte útil leer los pasos para desarrollar un componentes de flujo de datos personalizados en el [desarrollar un componente de flujo de datos personalizado](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) sección y especialmente [Desarrollar un componente de destino personalizado](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md).  
  
## <a name="getting-started-with-a-destination-component"></a>Introducción a un componente de destino  
 Al agregar un componente de Script a la pestaña flujo de datos de [!INCLUDE[ssIS](../../includes/ssis-md.md)] diseñador, el **seleccionar el tipo de componente de Script** cuadro de diálogo se abre y le pide que seleccione un **origen**, **destino** , o **transformación** secuencia de comandos. En este cuadro de diálogo, seleccione **destino**.  
  
 A continuación, conecte la salida de una transformación al componente de destino en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Como prueba, puede conectar un origen directamente a un destino sin ninguna transformación.  
  
## <a name="configuring-a-destination-component-in-metadata-design-mode"></a>Configurar un componente de destino en modo de diseño de metadatos  
 Después de seleccionar la opción para crear un componente de destino, configure el componente mediante el **Editor de transformación Script**. Para obtener más información, consulte [configurar el componente de Script en el Editor de componentes de secuencia de comandos](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Para seleccionar el lenguaje de script que se va a usar el destino de la secuencia de comandos, establezca la **ScriptLanguage** propiedad en el **Script** página de la **Editor de transformación Script** cuadro de diálogo.  
  
> [!NOTE]  
>  Para establecer el idioma para el componente de Script de scripting predeterminado, utilice la **lenguaje de Scripting** opción el **General** página de la **opciones** cuadro de diálogo. Para obtener más información, vea [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
 Un componente de destino de flujo de datos tiene una entrada y ninguna salida. Configurar la entrada del componente es uno de los pasos que debe completar en el modo de diseño de metadatos, mediante la **Editor de transformación Script**, antes de escribir un script personalizado.  
  
### <a name="adding-connection-managers"></a>Agregar administradores de conexión  
 Normalmente, un componente de destino utiliza un administrador de conexiones existente para conectarse al origen de datos donde guarda los datos del flujo de datos. En el **administradores de conexión** página de la **Editor de transformación Script**, haga clic en **agregar** para agregar el Administrador de conexiones adecuado.  
  
 Sin embargo, un administrador de conexiones es tan solo una unidad práctica que encapsula y almacena la información necesaria para conectarse a un origen de datos de un tipo determinado. Debe escribir su propio código personalizado para cargar o guardar los datos y posiblemente para abrir y cerrar la conexión al origen de datos.  
  
 Para obtener información general acerca de cómo se utilizan los administradores de conexión con el componente de Script, consulte [conectarse a orígenes de datos en el componente de Script](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md).  
  
 Para obtener más información sobre la **administradores de conexión** página de la **Editor de transformación Script**, consulte [Editor de transformación Script &#40; Página Administradores de conexión &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
### <a name="configuring-inputs-and-input-columns"></a>Configurar entradas y columnas de entrada  
 Un componente de destino tiene una entrada y ninguna salida.  
  
 En el **columnas de entrada** página de la **Editor de transformación Script**, la lista de columnas muestra las columnas disponibles de la salida del componente de nivel superior en el flujo de datos. Seleccione las columnas que desea guardar.  
  
 Para obtener más información sobre la **columnas de entrada** página de la **Editor de transformación Script**, consulte [Editor de transformación Script &#40; página columnas de entrada &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md).  
  
 El **entradas y salidas** página de la **Editor de transformación Script** muestra una entrada única, que se puede cambiar. Hará referencia a la entrada por su nombre en el script mediante la propiedad de descriptor de acceso creada en el código generado automáticamente.  
  
 Para obtener más información sobre la **entradas y salidas** página de la **Editor de transformación Script**, consulte [Editor de transformación Script &#40; entradas y salidas de página &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md).  
  
### <a name="adding-variables"></a>Agregar variables  
 Si desea utilizar variables existentes en el script, puede agregarlos en el **ReadOnlyVariables** y **ReadWriteVariables** campos de propiedades en el **Script** página de la **Editor de transformación script**.  
  
 Cuando agregue varias variables a los campos de propiedades, separe sus nombres con comas. También puede seleccionar varias variables, haga clic en el botón de puntos suspensivos (**...** ) situado junto a la **ReadOnlyVariables** y **ReadWriteVariables** campos de propiedades y, a continuación, seleccionar las variables en el **seleccionar variables** cuadro de diálogo.  
  
 Para obtener información general acerca de cómo usar variables con el componente de Script, consulte [usar Variables en el componente de Script](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Para obtener más información sobre la **Script** página de la **Editor de transformación Script**, consulte [Editor de transformación Script &#40; Página script &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-destination-component-in-code-design-mode"></a>Generar script en un componente de destino en modo de diseño de código  
 Después de haber configurado los metadatos para el componente, puede escribir un script personalizado. En el **Editor de transformación Script**, en la **Script** página, haga clic en **editar Script** para abrir el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools para aplicaciones (VSTA) IDE donde puede agregar un script personalizado. El lenguaje de scripting que utilice depende de si seleccionó [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# como lenguaje de script para la **ScriptLanguage** propiedad en el **Script** página.  
  
 Para obtener información importante que se aplica a todos los tipos de componentes creados mediante el componente de Script, consulte [codificar y depurar el componente de Script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Descripción del código generado automáticamente  
 Cuando se abre el IDE de VSTA después de crear y configurar un componente de destino, el editable **ScriptMain** clase aparece en el editor de código con un código auxiliar para la **ProcessInputRow** método. El **ScriptMain** clase es donde se escribirá el código personalizado, y **ProcessInputRow** es el método más importante en un componente de destino.  
  
 Si abre el **el Explorador de proyectos** ventana en VSTA, puede ver que el componente de Script también ha generado de solo lectura **BufferWrapper** y **ComponentWrapper** proyecto elementos. El **ScriptMain** clase hereda de **UserComponent** clase en el **ComponentWrapper** elemento de proyecto.  
  
 En tiempo de ejecución, el motor de flujo de datos, se invoca el **ProcessInput** método en el **UserComponent** de la clase, lo que invalida el <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> método de la <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> clase primaria. El **ProcessInput** método a su vez recorre las filas en el búfer de entrada y llama el **ProcessInputRow** método una vez por cada fila.  
  
### <a name="writing-your-custom-code"></a>Escribir código personalizado  
 Para terminar de crear un componente de destino personalizado, puede que desee escribir script en los siguientes métodos disponibles en la **ScriptMain** clase.  
  
1.  Invalidar el **AcquireConnections** método para conectarse al origen de datos externo. Extraiga el objeto de conexión, o la información de conexión necesaria, del administrador de conexiones.  
  
2.  Invalidar el **PreExecute** método para prepararse para guardar los datos. Por ejemplo, puede que desee crear y configurar un **SqlCommand** y sus parámetros de este método.  
  
3.  Use el invalidado **ProcessInputRow** método para copiar cada fila de entrada en el origen de datos externo. Por ejemplo, para un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino, puede copiar los valores de columna en los parámetros de un **SqlCommand** y ejecute el comando una vez por cada fila. Para un destino de archivo sin formato, puede escribir los valores de cada columna en un **StreamWriter**, separe los valores mediante el delimitador de columna.  
  
4.  Invalidar el **PostExecute** método para desconectarse del origen de datos externo, si es necesario y para realizar cualquier otra limpieza necesaria.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes muestran código que se requiere en el **ScriptMain** clase para crear un componente de destino.  
  
> [!NOTE]  
>  Estos ejemplos utilizan la **Person.Address** tabla el **AdventureWorks** base de datos de ejemplo y pasar sus columnas primeros y cuarto, la **int*AddressID*** y **nvarchar (30) Ciudad** columnas, a través del flujo de datos. Estos mismos datos se usan en los ejemplos de origen, transformación y destino de esta sección. Se documentan requisitos previos y suposiciones adicionales para cada ejemplo.  
  
### <a name="adonet-destination-example"></a>Ejemplo de destino ADO.NET  
 En este ejemplo se muestra un componente de destino que utiliza un archivo [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Administrador de conexiones para guardar los datos del flujo de datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla.  
  
 Si desea ejecutar este código de ejemplo, debe configurar el paquete y el componente de la siguiente forma:  
  
1.  Crear un [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Administrador de conexiones que usa el **SqlClient** proveedor para conectarse a la **AdventureWorks** base de datos.  
  
2.  Crear una tabla de destino ejecutando el siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] comando en el **AdventureWorks** base de datos:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  Agregue un nuevo componente de script a la superficie del diseñador de flujo de datos y configúrelo como destino.  
  
4.  Conecte la salida de un origen o transformación de nivel superior al componente de destino en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)]. (Puede conectar directamente un origen a un destino sin ninguna transformación.) Esta salida debe proporcionar datos de la **Person.Address** tabla de la **AdventureWorks** base de datos de ejemplo que contiene al menos el **AddressID** y  **Ciudad** columnas.  
  
5.  Abra la **Editor de transformación Script**. En el **columnas de entrada** página, seleccione la **AddressID** y **City** columnas de entrada.  
  
6.  En el **entradas y salidas** página, cambie el nombre de la entrada con un nombre más descriptivo como **MyAddressInput**.  
  
7.  En el **administradores de conexión** página, agregue o cree la [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Administrador de conexiones con un nombre como **MyADONETConnectionManager**.  
  
8.  En el **Script** página, haga clic en **editar Script** y escriba el script siguiente. A continuación, cierre el entorno de desarrollo de script.  
  
9. Cerrar la **Editor de transformación Script** y ejecutar el ejemplo.  
  
```vb  
Imports System.Data.SqlClient  
...  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Dim connMgr As IDTSConnectionManager100  
    Dim sqlConn As SqlConnection  
    Dim sqlCmd As SqlCommand  
    Dim sqlParam As SqlParameter  
  
    Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
        connMgr = Me.Connections.MyADONETConnectionManager  
        sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
    End Sub  
  
    Public Overrides Sub PreExecute()  
  
        sqlCmd = New SqlCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
            "VALUES(@addressid, @city)", sqlConn)  
        sqlParam = New SqlParameter("@addressid", SqlDbType.Int)  
        sqlCmd.Parameters.Add(sqlParam)  
        sqlParam = New SqlParameter("@city", SqlDbType.NVarChar, 30)  
        sqlCmd.Parameters.Add(sqlParam)  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
        With sqlCmd  
            .Parameters("@addressid").Value = Row.AddressID  
            .Parameters("@city").Value = Row.City  
            .ExecuteNonQuery()  
        End With  
    End Sub  
  
    Public Overrides Sub ReleaseConnections()  
  
        connMgr.ReleaseConnection(sqlConn)  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System.Data.SqlClient;  
public class ScriptMain:  
    UserComponent  
  
{  
    IDTSConnectionManager100 connMgr;  
    SqlConnection sqlConn;  
    SqlCommand sqlCmd;  
    SqlParameter sqlParam;  
  
    public override void AcquireConnections(object Transaction)  
    {  
  
        connMgr = this.Connections.MyADONETConnectionManager;  
        sqlConn = (SqlConnection)connMgr.AcquireConnection(null);  
  
    }  
  
    public override void PreExecute()  
    {  
  
        sqlCmd = new SqlCommand("INSERT INTO Person.Address2(AddressID, City) " +  
            "VALUES(@addressid, @city)", sqlConn);  
        sqlParam = new SqlParameter("@addressid", SqlDbType.Int);  
        sqlCmd.Parameters.Add(sqlParam);  
        sqlParam = new SqlParameter("@city", SqlDbType.NVarChar, 30);  
        sqlCmd.Parameters.Add(sqlParam);  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
        {  
            sqlCmd.Parameters["@addressid"].Value = Row.AddressID;  
            sqlCmd.Parameters["@city"].Value = Row.City;  
            sqlCmd.ExecuteNonQuery();  
        }  
    }  
  
    public override void ReleaseConnections()  
    {  
  
        connMgr.ReleaseConnection(sqlConn);  
  
    }  
  
}  
```  
  
### <a name="flat-file-destination-example"></a>Ejemplo de destino de archivo plano  
 En este ejemplo se muestra un componente de destino que utiliza un administrador de conexiones de archivos planos existente para guardar datos del flujo de datos en un archivo plano.  
  
 Si desea ejecutar este código de ejemplo, debe configurar el paquete y el componente de la siguiente forma:  
  
1.  Cree un administrador de conexiones de archivos planos que conecte a un archivo de destino. El archivo no tiene que existir; el componente de destino lo creará. Configure el archivo de destino como un archivo delimitado por comas que contiene la **AddressID** y **City** columnas.  
  
2.  Agregue un nuevo componente de script a la superficie del diseñador de flujo de datos y configúrelo como destino.  
  
3.  Conecte la salida de un origen o transformación de nivel superior al componente de destino en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)]. (Puede conectar directamente un origen a un destino sin ninguna transformación.) Esta salida debe proporcionar datos de la **Person.Address** tabla de la **AdventureWorks** base de datos de ejemplo y debe contener al menos el **AddressID** y **City** columnas.  
  
4.  Abra la **Editor de transformación Script**. En el **columnas de entrada** página, seleccione la **AddressID** y **City** columnas.  
  
5.  En el **entradas y salidas** página, cambie el nombre de la entrada con un nombre más descriptivo, como **MyAddressInput**.  
  
6.  En el **administradores de conexión** página, agregue o cree la conexión de archivos planos Administrador con un nombre descriptivo como **MyFlatFileDestConnectionManager**.  
  
7.  En el **Script** página, haga clic en **editar Script** y escriba el script siguiente. A continuación, cierre el entorno de desarrollo de script.  
  
8.  Cerrar la **Editor de transformación Script** y ejecutar el ejemplo.  
  
```vb  
Imports System.IO  
...  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Dim copiedAddressFile As String  
    Private textWriter As StreamWriter  
    Private columnDelimiter As String = ","  
  
    Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
        Dim connMgr As IDTSConnectionManager100 = _  
            Me.Connections.MyFlatFileDestConnectionManager  
        copiedAddressFile = CType(connMgr.AcquireConnection(Nothing), String)  
  
    End Sub  
  
    Public Overrides Sub PreExecute()  
  
        textWriter = New StreamWriter(copiedAddressFile, False)  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        With textWriter  
            If Not Row.AddressID_IsNull Then  
                .Write(Row.AddressID)  
            End If  
            .Write(columnDelimiter)  
            If Not Row.City_IsNull Then  
                .Write(Row.City)  
            End If  
            .WriteLine()  
        End With  
  
    End Sub  
  
    Public Overrides Sub PostExecute()  
  
        textWriter.Close()  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System.IO;  
public class ScriptMain:  
    UserComponent  
  
{  
    string copiedAddressFile;  
    private StreamWriter textWriter;  
    private string columnDelimiter = ",";  
  
    public override void AcquireConnections(object Transaction)  
    {  
  
        IDTSConnectionManager100 connMgr = this.Connections.MyFlatFileDestConnectionManager;  
        copiedAddressFile = (string) connMgr.AcquireConnection(null);  
  
    }  
  
    public override void PreExecute()  
    {  
  
        textWriter = new StreamWriter(copiedAddressFile, false);  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        {  
            if (!Row.AddressID_IsNull)  
            {  
                textWriter.Write(Row.AddressID);  
            }  
            textWriter.Write(columnDelimiter);  
            if (!Row.City_IsNull)  
            {  
                textWriter.Write(Row.City);  
            }  
            textWriter.WriteLine();  
        }  
  
    }  
  
    public override void PostExecute()  
    {  
  
        textWriter.Close();  
  
    }  
  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Crear un origen con el componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)   
 [Desarrollar un componente de destino personalizado](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
  
  


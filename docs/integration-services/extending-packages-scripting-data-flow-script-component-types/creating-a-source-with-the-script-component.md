---
title: Crear un origen con el componente de Script | Documentos de Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting-data-flow-script-component-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], source components
- output columns [Integration Services]
- sources [Integration Services], components
ms.assetid: 547c4179-ea82-4265-8c6f-04a2aa77a3c0
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d4944c3d5752da21fed90f16a38a33b4fad41515
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="creating-a-source-with-the-script-component"></a>Crear un origen con el componente de script
  Los componentes de origen del flujo de datos de un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se usan para cargar datos de un origen de datos y pasarlos a transformaciones y destinos de nivel inferior. Normalmente la conexión al origen de datos se realiza a través de un administrador de conexiones existente.  
  
 Para obtener información general del componente de Script, consulte [extender el flujo de datos con el componente de Script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
 El componente de script y el código de infraestructura que genera simplifican considerablemente el proceso de desarrollo de un componente de flujo de datos personalizado. Sin embargo, para entender cómo funciona el componente de script, puede resultar útil leer los pasos necesarios para el desarrollo de un componente de flujo de datos personalizado. Vea la sección [desarrollar un componente de flujo de datos personalizada](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md), especialmente el tema [desarrollar un componente de origen personalizado](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md).  
  
## <a name="getting-started-with-a-source-component"></a>Introducción al componente de origen  
 Al agregar un componente de Script al panel flujo de datos de [!INCLUDE[ssIS](../../includes/ssis-md.md)] diseñador, el **seleccionar el tipo de componente de Script** cuadro de diálogo se abre y le pide que seleccione una secuencia de comandos de origen, destino o transformación. En este cuadro de diálogo, seleccione **origen**.  
  
## <a name="configuring-a-source-component-in-metadata-design-mode"></a>Configurar un componente de origen en modo de diseño de metadatos  
 Después de seleccionar esta opción para crear un componente de origen, configure el componente mediante el **Editor de transformación Script**. Para obtener más información, consulte [configurar el componente de Script en el Editor de componentes de secuencia de comandos](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Un componente de origen de flujo de datos no tiene ninguna entrada y admite una o más salidas. Configurar las salidas del componente es uno de los pasos que debe completar en el modo de diseño de metadatos, mediante la **Editor de transformación Script**, antes de escribir un script personalizado.  
  
 También puede especificar el lenguaje de script estableciendo la **ScriptLanguage** propiedad en el **Script** página de la **Editor de transformación Script**.  
  
> [!NOTE]  
>  Para establecer el lenguaje de script predeterminado para los componentes de Script y las tareas Script, utilice la **lenguaje de Scripting** opción el **General** página de la **opciones** cuadro de diálogo. Para obtener más información, vea [General Page](~/integration-services/control-flow/script-task-editor-general-page.md).  
  
### <a name="adding-connection-managers"></a>Agregar administradores de conexión  
 Normalmente, un componente de origen utiliza un administrador de conexiones existente para conectarse al origen de datos del que carga los datos en el flujo de datos. En el **administradores de conexión** página de la **Editor de transformación Script**, haga clic en **agregar** para agregar el Administrador de conexiones adecuado.  
  
 Sin embargo, un administrador de conexiones solo es una unidad práctica que encapsula y almacena la información necesaria para conectarse a un origen de datos de un tipo determinado. Debe escribir su propio código personalizado para cargar o guardar los datos y posiblemente también para abrir y cerrar la conexión al origen de datos.  
  
 Para obtener información general acerca de cómo se utilizan los administradores de conexión con el componente de Script, consulte [conectarse a orígenes de datos en el componente de Script](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md).  
  
 Para obtener más información sobre la **administradores de conexión** página de la **Editor de transformación Script**, consulte [Editor de transformación Script &#40; Página Administradores de conexión &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
### <a name="configuring-outputs-and-output-columns"></a>Configurar salidas y columnas de salida  
 Un componente de origen no tiene ninguna entrada y admite una o más salidas. En el **entradas y salidas** página de la **Editor de transformación Script**, se ha creado una salida única de forma predeterminada, pero no se ha creado ninguna columna de salida. En esta página del editor, quizá necesite o desee configurar los elementos siguientes.  
  
-   Debe agregar y configurar manualmente las columnas de salida para cada salida. Seleccione la carpeta de las columnas de salida para cada salida y, a continuación, use la **Agregar columna** y **Quitar columna** botones para administrar las columnas de salida para cada salida del componente de origen. Después, hará referencia a las columnas de salida en el script por los nombres que asigna aquí, mediante las propiedades de descriptor de acceso con tipo creadas en el código generado automáticamente.  
  
-   Puede crear una o varias salidas adicionales, como una salida de error simulada para las filas que contienen valores inesperados. Use la **agregar salida** y **quitar salida** botones para administrar las salidas del componente de origen. Todas las filas de entrada se dirigen a todas las salidas disponibles a menos que también especifique un valor distinto de cero idéntico para el **ExclusionGroup** propiedad de estas salidas donde desea dirigir cada fila a solo una de las salidas que comparten el mismo **ExclusionGroup** valor. El valor entero determinado seleccionado para identificar la **ExclusionGroup** no es significativo.  
  
    > [!NOTE]  
    >  También puede utilizar un elemento que es distinto de cero **ExclusionGroup** valor de propiedad con una salida única si no desea todas las filas de salida. En este caso, sin embargo, debe llamar explícitamente a la **DirectRowTo\<outputbuffer >** método para cada fila que se desea enviar a la salida.  
  
-   Puede asignar un nombre descriptivo a las salidas. Después, hará referencia a las salidas en el script por sus nombres, mediante las propiedades de descriptor de acceso con tipo creadas en el código generado automáticamente.  
  
-   Normalmente, varias salidas en la misma **ExclusionGroup** tener el mismo columnas de salida. Sin embargo, si crea una salida de error simulada, quizá desee agregar más columnas que almacenen información de error. Para obtener información acerca de cómo el flujo de datos motor procesa las filas de error, consulte [uso de salidas de Error en un componente de flujo de datos](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md). En el componente de script, sin embargo, debe escribir su propio código para llenar las columnas adicionales con la información de error adecuada. Para obtener más información, consulte [simular una salida de Error para el componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).  
  
 Para obtener más información sobre la **entradas y salidas** página de la **Editor de transformación Script**, consulte [Editor de transformación Script &#40; entradas y salidas de página &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md).  
  
### <a name="adding-variables"></a>Agregar variables  
 Si hay cualquier variables existentes cuyos valores desea utilizar en la secuencia de comandos, puede agregarlos en el **ReadOnlyVariables** y **ReadWriteVariables** campos de propiedades el **Script** página de la **Editor de transformación Script**.  
  
 Al introducir diversas variables en los campos de propiedades, separe los nombres de éstas por comas. También puede especificar varias variables haciendo clic en los puntos suspensivos (**...** ) situado junto a la **ReadOnlyVariables** y **ReadWriteVariables** campos de propiedades y seleccione las variables de la **seleccionar variables** cuadro de diálogo .  
  
 Para obtener información general acerca de cómo usar variables con el componente de Script, consulte [usar Variables en el componente de Script](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Para obtener más información sobre la **Script** página de la **Editor de transformación Script**, consulte [Editor de transformación Script &#40; Página script &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-source-component-in-code-design-mode"></a>Generar script en un componente de origen en modo de diseño de código  
 Después de haber configurado los metadatos para el componente, abra el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools para aplicaciones (VSTA) IDE que se va a codificar el script personalizado. Para abrir VSTA, haga clic en **editar Script** en el **Script** página de la **Editor de transformación Script**. Puede escribir la secuencia de comandos mediante [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#, dependiendo del lenguaje de script seleccionado para la **ScriptLanguage** propiedad.  
  
 Para obtener información importante que se aplica a todos los tipos de componentes creados mediante el componente de Script, consulte [codificar y depurar el componente de Script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Descripción del código generado automáticamente  
 Al abrir el IDE de VSTA después de crear y configurar un componente de origen, el editable **ScriptMain** clase aparece en el editor de código. Escribir el código personalizado el **ScriptMain** clase.  
  
 El **ScriptMain** clase incluye un código auxiliar para la **CreateNewOutputRows** método. El **CreateNewOutputRows** es el método más importante en un componente de origen.  
  
 Si abre el **el Explorador de proyectos** ventana en VSTA, puede ver que el componente de Script también ha generado de solo lectura **BufferWrapper** y **ComponentWrapper** proyecto elementos. El **ScriptMain** clase hereda de **UserComponent** clase en el **ComponentWrapper** elemento de proyecto.  
  
 En tiempo de ejecución, el motor de flujo de datos, se invoca el **PrimeOutput** método en el **UserComponent** de la clase, lo que invalida el <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PrimeOutput%2A> método de la <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> clase primaria. El **PrimeOutput** método a su vez llama a los métodos siguientes:  
  
1.  El **CreateNewOutputRows** método, que invalide en **ScriptMain** para agregar filas del origen de datos a la salida de búferes, que son vacío al principio.  
  
2.  El **FinishOutputs** método, que está vacía de forma predeterminada. Invalide este método en **ScriptMain** para realizar cualquier procesamiento necesario para completar la salida.  
  
3.  Privado **MarkOutputsAsFinished** método, que llama a la <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.SetEndOfRowset%2A> método de la <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> clase para indicar al motor de flujo de datos que ha finalizado el resultado principal. No es necesario llamar a **SetEndOfRowset** explícitamente en su propio código.  
  
### <a name="writing-your-custom-code"></a>Escribir código personalizado  
 Para terminar de crear un componente de origen personalizado, puede que desee escribir script en los siguientes métodos disponibles en la **ScriptMain** clase.  
  
1.  Invalidar el **AcquireConnections** método para conectarse al origen de datos externo. Extraiga el objeto de conexión, o la información de conexión necesaria, del administrador de conexiones.  
  
2.  Invalidar el **PreExecute** método para cargar datos, si puede cargar todos los datos de origen al mismo tiempo. Por ejemplo, puede ejecutar una **SqlCommand** contra un [!INCLUDE[vstecado](../../includes/vstecado-md.md)] conexión a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la base de datos y cargar todos los datos de origen al mismo tiempo en un **SqlDataReader**. Si debe cargar el fila de un origen de datos a la vez (por ejemplo, al leer un archivo de texto), puede cargar los datos como recorrer las filas de **CreateNewOutputRows**.  
  
3.  Use el invalidado **CreateNewOutputRows** método para agregar nuevas filas a los búferes de salida vacíos y rellenar los valores de cada columna en las nuevas filas de salida. Use la **AddRow** método de cada búfer de salida para agregar una nueva fila vacía y, a continuación, establezca los valores de cada columna. Normalmente copia los valores de las columnas cargadas del origen externo.  
  
4.  Invalidar el **PostExecute** método termine de procesar los datos. Por ejemplo, puede cerrar la **SqlDataReader** que usa para cargar datos.  
  
5.  Invalidar el **ReleaseConnections** método para desconectarse del origen de datos externo, si es necesario.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes muestran el código personalizado que se requiere en el **ScriptMain** clase para crear un componente de origen.  
  
> [!NOTE]  
>  Estos ejemplos utilizan la **Person.Address** tabla el **AdventureWorks** base de datos de ejemplo y pasar sus columnas primeros y cuarto, la **intAddressID** y  **nvarchar (30) Ciudad** columnas, a través del flujo de datos. Estos mismos datos se usan en los ejemplos de origen, transformación y destino de esta sección. Se documentan requisitos previos y suposiciones adicionales para cada ejemplo.  
  
### <a name="adonet-source-example"></a>Ejemplo de origen de ADO.NET  
 En este ejemplo se muestra un componente de origen que utiliza un archivo [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Administrador de conexiones para cargar datos desde un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla en el flujo de datos.  
  
 Si desea ejecutar este código de ejemplo, debe configurar el paquete y el componente de la siguiente forma:  
  
1.  Crear un [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Administrador de conexiones que usa el **SqlClient** proveedor para conectarse a la **AdventureWorks** base de datos.  
  
2.  Agregue un nuevo componente de script a la superficie del diseñador de flujo de datos y configúrelo como origen.  
  
3.  Abra la **Editor de transformación Script**. En el **entradas y salidas** página, cambie el nombre de la salida predeterminada por un nombre más descriptivo como **MyAddressOutput**y agregue y configure las dos columnas de salida, **AddressID**y **City**.  
  
    > [!NOTE]  
    >  No olvide cambiar el tipo de datos de la **City** columna de salida a DT_WSTR.  
  
4.  En el **administradores de conexión** página, agregue o cree la [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Administrador de conexiones y asígnele un nombre como **MyADONETConnection**.  
  
5.  En el **Script** página, haga clic en **editar Script** y escriba el script siguiente. A continuación, cierre el entorno de desarrollo de script y el **Editor de transformación Script**.  
  
6.  Crear y configurar un componente de destino, como un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino o el componente de destino de ejemplo que muestra en [crear un destino con el componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md), que espera la  **AddressID** y **City** columnas. A continuación, conecte el componente de origen al destino. (Puede conectar directamente un origen a un destino sin ninguna transformación.) Puede crear una tabla de destino ejecutando el siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] comando en el **AdventureWorks** base de datos:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
7.  Ejecute el ejemplo.  
  
    ```vb  
    Imports System.Data.SqlClient  
    ...  
    Public Class ScriptMain  
        Inherits UserComponent  
  
        Dim connMgr As IDTSConnectionManager100  
        Dim sqlConn As SqlConnection  
        Dim sqlReader As SqlDataReader  
  
        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
            connMgr = Me.Connections.MyADONETConnection  
            sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
        End Sub  
  
        Public Overrides Sub PreExecute()  
  
            Dim cmd As New SqlCommand("SELECT AddressID, City, StateProvinceID FROM Person.Address", sqlConn)  
            sqlReader = cmd.ExecuteReader  
  
        End Sub  
  
        Public Overrides Sub CreateNewOutputRows()  
  
            Do While sqlReader.Read  
                With MyAddressOutputBuffer  
                    .AddRow()  
                    .AddressID = sqlReader.GetInt32(0)  
                    .City = sqlReader.GetString(1)  
                End With  
            Loop  
  
        End Sub  
  
        Public Overrides Sub PostExecute()  
  
            sqlReader.Close()  
  
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
        SqlDataReader sqlReader;  
  
        public override void AcquireConnections(object Transaction)  
        {  
            connMgr = this.Connections.MyADONETConnection;  
            sqlConn = (SqlConnection)connMgr.AcquireConnection(null);  
  
        }  
  
        public override void PreExecute()  
        {  
  
            SqlCommand cmd = new SqlCommand("SELECT AddressID, City, StateProvinceID FROM Person.Address", sqlConn);  
            sqlReader = cmd.ExecuteReader();  
  
        }  
  
        public override void CreateNewOutputRows()  
        {  
  
            while (sqlReader.Read())  
            {  
                {  
                    MyAddressOutputBuffer.AddRow();  
                    MyAddressOutputBuffer.AddressID = sqlReader.GetInt32(0);  
                    MyAddressOutputBuffer.City = sqlReader.GetString(1);  
                }  
            }  
  
        }  
  
        public override void PostExecute()  
        {  
  
            sqlReader.Close();  
  
        }  
  
        public override void ReleaseConnections()  
        {  
  
            connMgr.ReleaseConnection(sqlConn);  
  
        }  
  
    }  
    ```  
  
### <a name="flat-file-source-example"></a>Ejemplo de origen de archivo plano  
 En este ejemplo se muestra un componente de origen que utiliza un administrador de conexiones de archivos planos existente para cargar datos de un archivo plano en el flujo de datos. Los datos de origen del archivo plano se crean mediante su exportación desde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Si desea ejecutar este código de ejemplo, debe configurar el paquete y el componente de la siguiente forma:  
  
1.  Use la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import and Export Wizard para exportar la **Person.Address** tabla desde el **AdventureWorks** base de datos de ejemplo en un archivo sin formato delimitado por comas. En este ejemplo se utiliza el nombre de archivo ExportedAddresses.txt.  
  
2.  Cree un administrador de conexiones de archivos planos que se conecte al archivo de datos exportado.  
  
3.  Agregue un nuevo componente de script a la superficie del diseñador de flujo de datos y configúrelo como origen.  
  
4.  Abra la **Editor de transformación Script**. En el **entradas y salidas** página, cambie el nombre de la salida predeterminada por un nombre más descriptivo como **MyAddressOutput**. Agregue y configure las dos columnas de salida, **AddressID** y **City**.  
  
5.  En el **administradores de conexión** página, agregue o cree la conexión de archivos planos administrador, con un nombre descriptivo como **MyFlatFileSrcConnectionManager**.  
  
6.  En el **Script** página, haga clic en **editar Script** y escriba el script siguiente. A continuación, cierre el entorno de desarrollo de script y el **Editor de transformación Script**.  
  
7.  Crear y configurar un componente de destino, como un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino o el componente de destino de ejemplo que muestra en [crear un destino con el componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md). A continuación, conecte el componente de origen al destino. (Puede conectar directamente un origen a un destino sin ninguna transformación.) Puede crear una tabla de destino ejecutando el siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] comando en el **AdventureWorks** base de datos:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
8.  Ejecute el ejemplo.  
  
    ```vb  
    Imports System.IO  
    ...  
    Public Class ScriptMain  
        Inherits UserComponent  
  
        Private textReader As StreamReader  
        Private exportedAddressFile As String  
  
        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
            Dim connMgr As IDTSConnectionManager100 = _  
                Me.Connections.MyFlatFileSrcConnectionManager  
            exportedAddressFile = _  
                CType(connMgr.AcquireConnection(Nothing), String)  
  
        End Sub  
  
        Public Overrides Sub PreExecute()  
            MyBase.PreExecute()  
            textReader = New StreamReader(exportedAddressFile)  
        End Sub  
  
        Public Overrides Sub CreateNewOutputRows()  
  
            Dim nextLine As String  
            Dim columns As String()  
  
            Dim delimiters As Char()  
            delimiters = ",".ToCharArray  
  
            nextLine = textReader.ReadLine  
            Do While nextLine IsNot Nothing  
                columns = nextLine.Split(delimiters)  
                With MyAddressOutputBuffer  
                    .AddRow()  
                    .AddressID = columns(0)  
                    .City = columns(3)  
                End With  
                nextLine = textReader.ReadLine  
            Loop  
  
        End Sub  
  
        Public Overrides Sub PostExecute()  
            MyBase.PostExecute()  
            textReader.Close()  
  
        End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System.IO;  
    public class ScriptMain:  
        UserComponent  
  
    {  
        private StreamReader textReader;  
        private string exportedAddressFile;  
  
        public override void AcquireConnections(object Transaction)  
        {  
  
            IDTSConnectionManager100 connMgr = this.Connections.MyFlatFileSrcConnectionManager;  
            exportedAddressFile = (string)connMgr.AcquireConnection(null);  
  
        }  
  
        public override void PreExecute()  
        {  
            base.PreExecute();  
            textReader = new StreamReader(exportedAddressFile);  
        }  
  
        public override void CreateNewOutputRows()  
        {  
  
            string nextLine;  
            string[] columns;  
  
            char[] delimiters;  
            delimiters = ",".ToCharArray();  
  
            nextLine = textReader.ReadLine();  
            while (nextLine != null)  
            {  
                columns = nextLine.Split(delimiters);  
                {  
                    MyAddressOutputBuffer.AddRow();  
                    MyAddressOutputBuffer.AddressID = columns[0];  
                    MyAddressOutputBuffer.City = columns[3];  
                }  
                nextLine = textReader.ReadLine();  
            }  
  
        }  
  
        public override void PostExecute()  
        {  
  
            base.PostExecute();  
            textReader.Close();  
  
        }  
  
    }  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Crear un destino con el componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)   
 [Desarrollar un componente de origen personalizado](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
  
  


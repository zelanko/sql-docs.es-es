---
title: Incorporar una tarea de generación de perfiles de datos en un flujo de trabajo de paquetes | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling task [Integration Services], using output in workflow
ms.assetid: 39a51586-6977-4c45-b80b-0157a54ad510
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9acb58bf89d23e58ac23f96141f2a5b4dd551019
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "71294120"
---
# <a name="incorporate-a-data-profiling-task-in-package-workflow"></a>Incorporar una tarea de generación de perfiles de datos en un flujo de trabajo de paquetes

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La generación de perfiles de datos y la limpieza no son aptos para la aplicación de un proceso automatizado en sus primeras etapas. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], el resultado de la tarea de generación de perfiles de datos normalmente requiere un análisis visual y un criterio humano para determinar si las infracciones detectadas son significativas o excesivas. Incluso después de reconocer la existencia de problemas relacionados con la calidad de los datos, sigue siendo necesario disponer de un plan minuciosamente diseñado que indique el mejor método para la limpieza.  
  
 Sin embargo, una vez establecidos los criterios para la calidad de los datos, es posible que desee automatizar el análisis y la limpieza periódicos del origen de datos. Considere estos escenarios:  
  
-   **Comprobar la calidad de los datos antes de una carga incremental**. Use la tarea de generación de perfiles de datos para calcular el perfil de proporción de columnas nulas de los nuevos datos para la columna CustomerName de una tabla Customers. Si el porcentaje de valores NULL es superior al 20%, envíe al operador un mensaje de correo electrónico que contenga los resultados del perfil y finalice el paquete. En caso contrario, continúe con la carga incremental.  
  
-   **Automatizar la limpieza cuando se cumplen las condiciones especificadas**. Use la tarea de generación de perfiles de datos para calcular el perfil de inclusión de valores de la columna State en una tabla de búsqueda de estados, y el de la columna ZIP Code/Postal Code en una tabla de búsqueda de códigos postales. Si el nivel de inclusión de los valores de estado es inferior al 80%, pero el de los valores de código postal es superior al 99%, esto indica dos cosas. En primer lugar, los datos de estado están dañados. En segundo lugar, los datos de código postal están en buen estado. Inicie una tarea Flujo de datos que limpie los datos de estado realizando una búsqueda de los valores de estado correctos a partir de los valores de código postal actuales.  
  
 Una vez que disponga de un flujo de trabajo en el que pueda incorporar la tarea Flujo de datos, deberá comprender los pasos requeridos para agregar esta tarea. En la sección siguiente se describe el proceso general de incorporación de la tarea Flujo de datos. Las dos secciones finales describen cómo conectar la tarea Flujo de datos directamente a un origen de datos o a datos transformados del flujo de datos.  
  
## <a name="defining-a-general-workflow-for-the-data-flow-task"></a>Definir un flujo de trabajo general para la tarea Flujo de datos  
 En el procedimiento siguiente se describe el método general para usar el resultado de la tarea de generación de perfiles de datos en el flujo de trabajo de un paquete.  
  
#### <a name="to-use-the-output-of-the-data-profiling-task-programmatically-in-a-package"></a>Para usar el resultado de la tarea de generación de perfiles de datos en un paquete mediante programación  
  
1.  Agregue y configure la tarea de generación de perfiles de datos en un paquete.  
  
2.  Configure las variables de paquete que van a contener los valores que desea recuperar de los resultados del perfil.  
  
3.  Agregue y configure una tarea Script. Conecte dicha tarea a la tarea de generación de perfiles de datos. En la tarea Script, escriba el código necesario para leer los valores deseados del archivo de resultados de la tarea de generación de perfiles de datos y rellenar las variables de paquete.  
  
4.  En las restricciones de precedencia que conectan la tarea Script a las bifurcaciones de nivel inferior del flujo de trabajo, escriba expresiones que usen los valores de las variables para dirigir el flujo de trabajo.  
  
 Al incorporar la tarea de generación de perfiles de datos al flujo de trabajo de un paquete, tenga en cuenta estas dos características de dicha tarea:  
  
-   **Resultado de la tarea**. La tarea de generación de perfiles de datos escribe su resultado en un archivo o en una variable de paquete en el formato XML, de acuerdo con el esquema DataProfile.xsd. Por lo tanto, si desea usar los resultados del perfil en el flujo de trabajo condicional del paquete, debe realizar una consulta en los resultados XML. Para ello, puede usar el lenguaje para consultas Xpath. Para estudiar la estructura de estos resultados XML, puede abrir un archivo de resultados de ejemplo o el propio esquema. Para abrir el archivo de salida o el esquema, puede usar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], otro editor XML o un editor de texto, como el Bloc de notas.  
  
    > [!NOTE]  
    >  Algunos de los resultados del perfil que se muestran en el Visor de perfil de datos son valores calculados que no se encuentran directamente en la salida. Por ejemplo, la salida del perfil de proporción de columnas nulas contiene el número total de filas y el número de filas que contienen valores NULL. Para obtener la proporción de columnas nulas, debe usar estos dos valores con objeto de calcular el porcentaje de filas que contienen valores NULL.  
  
-   **Entrada de la tarea**. La tarea de generación de perfiles de datos obtiene su entrada de tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por lo tanto, si desea generar perfiles de datos que ya se han cargado y transformado en el flujo de datos, debe guardar en tablas de ensayo los datos que están en la memoria.  
  
 En las siguientes secciones se aplica este flujo de trabajo general a la generación de perfiles de datos que proceden directamente de un origen de datos externo o que han sido transformados por la tarea Flujo de datos. En dichas secciones también se muestra cómo controlar los requisitos de entrada y salida de la tarea Flujo de datos.  
  
## <a name="connecting-the-data-profiling-task-directly-to-an-external-data-source"></a>Conectar directamente la tarea de generación de perfiles de datos a un origen de datos externo  
 La tarea de generación de perfiles de datos puede generar perfiles de los datos que provienen directamente de un origen de datos.  Para ilustrar esta capacidad, el ejemplo siguiente usa la tarea de generación de perfiles de datos para calcular un perfil de proporción de columnas nulas en las columnas de la tabla Person.Address de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] . A continuación, el ejemplo utiliza una tarea Script para recuperar los resultados del archivo de resultados y rellenar las variables de paquete que se pueden usar para dirigir el flujo de trabajo.  
  
> [!NOTE]  
>  Se ha seleccionado la columna AddressLine2 para este sencillo ejemplo porque contiene un alto porcentaje de valores NULL.  
  
 El ejemplo consta de los pasos siguientes:  
  
-   Configurar los administradores de conexión que se conectan al origen de datos externo y al archivo de resultados que contendrá los resultados del perfil.  
  
-   Configurar las variables de paquete que contendrán los valores requeridos por la tarea de generación de perfiles de datos.  
  
-   Configurar la tarea de generación de perfiles de datos para calcular el perfil de proporción de columnas nulas.  
  
-   Configurar la tarea Script para obtener la salida XML de la tarea de generación de perfiles de datos.  
  
-   Configurar las restricciones de precedencia que controlarán las bifurcaciones de nivel inferior del flujo de trabajo que se ejecutan dependiendo de los resultados de la tarea de generación de perfiles de datos.  
  
### <a name="configure-the-connection-managers"></a>Configurar los administradores de conexión  
 En este ejemplo hay dos administradores de conexión:  
  
-   Un administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] que se conecta a la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] .  
  
-   Un administrador de conexiones de archivos que crea el archivo de resultados que contendrá los resultados de la tarea de generación de perfiles de datos.  
  
##### <a name="to-configure-the-connection-managers"></a>Para configurar los administradores de conexión  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], cree un nuevo paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  Agregue un administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] al paquete. Configure dicho administrador de conexiones de forma que use el Proveedor de datos .NET para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) y se conecte a una instancia disponible de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] .  
  
     De forma predeterminada, el administrador de conexiones tiene el nombre siguiente: \<nombre de servidor>.AdventureWorks1.  
  
3.  Agregue un administrador de conexiones de archivos al paquete. Configure este administrador de conexiones con objeto de crear el archivo de resultados para la tarea de generación de perfiles de datos.  
  
     En este ejemplo se usa el nombre de archivo DataProfile1.xml. De forma predeterminada, el administrador de conexiones tiene el mismo nombre que el archivo.  
  
### <a name="configure-the-package-variables"></a>Configurar las variables de paquete  
 En este ejemplo se usan dos variables de paquete:  
  
-   La variable ProfileConnectionName pasa el nombre del administrador de conexiones de archivos a la tarea Script.  
  
-   La variable AddressLine2NullRatio pasa al paquete la proporción de columnas nulas calculada para esta columna por la tarea Script.  
  
##### <a name="to-configure-the-package-variables-that-will-hold-profile-results"></a>Para configurar las variables de paquete que almacenarán los resultados del perfil  
  
-   En la ventana **Variables** , agregue y configure las dos variables de paquete siguientes:  
  
    -   Escriba el nombre, **ProfileConnectionName**, para una de las variables y establezca el tipo de esta variable en **String**.  
  
    -   Escriba el nombre, **AddressLine2NullRatio**, para la otra variable y establezca el tipo de esta en **Double**.  
  
### <a name="configure-the-data-profiling-task"></a>Configurar la tarea de generación de perfiles de datos  
 La tarea de generación de perfiles de datos se debe configurar de la siguiente manera:  
  
-   Para que use los datos que el administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] especifica como entrada.  
  
-   Para que lleve a cabo un perfil de proporción de columnas nulas en los datos de entrada.  
  
-   Para que guarde los resultados del perfil en el archivo asociado al administrador de conexiones de archivos.  
  
##### <a name="to-configure-the-data-profiling-task"></a>Para configurar la tarea de generación de perfiles de datos  
  
1.  Agregue una tarea de generación de perfiles de datos al flujo de control.  
  
2.  Abra el **Editor de tareas de generación de perfiles de datos** para configurar la tarea.  
  
3.  En la página **General** del editor, en **Destino**, seleccione el nombre del administrador de conexiones de archivos configurado previamente.  
  
4.  En la página **Solicitudes de perfil** del editor, cree un nuevo perfil de proporción de columnas nulas.  
  
5.  En el panel **Propiedades de la solicitud** , en **ConnectionManager**, seleccione el administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] configurado previamente. A continuación, en **TableOrView**, seleccione Person.Address.  
  
6.  Cierre el Editor de tareas de generación de perfiles de datos.  
  
### <a name="configure-the-script-task"></a>Configurar la tarea Script  
 Debe configurarse la tarea Script para que recupere los resultados del archivo de resultados y rellene las variables de paquete previamente configuradas.  
  
##### <a name="to-configure-the-script-task"></a>Para configurar la tarea Script  
  
1.  Agregue una tarea Script al flujo de control.  
  
2.  Conecte dicha tarea a la tarea de generación de perfiles de datos.  
  
3.  Abra el **Editor de la tarea Script** para configurar la tarea.  
  
4.  En la página **Script** , seleccione el lenguaje de programación que prefiera. A continuación, ponga las dos variables de paquete a disposición del script:  
  
    1.  Para **ReadOnlyVariables**, seleccione **ProfileConnectionName**.  
  
    2.  Para **ReadWriteVariables**, seleccione **AddressLine2NullRatio**.  
  
5.  Seleccione **Editar script** para abrir el entorno de desarrollo de script.  
  
6.  Agregue una referencia al espacio de nombres System.Xml.  
  
7.  Escriba el código de ejemplo correspondiente al lenguaje de programación elegido:  
  
    ```vb  
    Imports System  
    Imports Microsoft.SqlServer.Dts.Runtime  
    Imports System.Xml  
  
    Public Class ScriptMain  
  
      Private FILENAME As String = "C:\ TEMP\DataProfile1.xml"  
      Private PROFILE_NAMESPACE_URI As String = "https://schemas.microsoft.com/DataDebugger/"  
      Private NULLCOUNT_XPATH As String = _  
        "/default:DataProfile/default:DataProfileOutput/default:Profiles" & _  
        "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:NullCount/text()"  
      Private TABLE_XPATH As String = _  
        "/default:DataProfile/default:DataProfileOutput/default:Profiles" & _  
        "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:Table"  
  
      Public Sub Main()  
  
        Dim profileConnectionName As String  
        Dim profilePath As String  
        Dim profileOutput As New XmlDocument  
        Dim profileNSM As XmlNamespaceManager  
        Dim nullCountNode As XmlNode  
        Dim nullCount As Integer  
        Dim tableNode As XmlNode  
        Dim rowCount As Integer  
        Dim nullRatio As Double  
  
        ' Open output file.  
        profileConnectionName = Dts.Variables("ProfileConnectionName").Value.ToString()  
        profilePath = Dts.Connections(profileConnectionName).ConnectionString  
        profileOutput.Load(profilePath)  
        profileNSM = New XmlNamespaceManager(profileOutput.NameTable)  
        profileNSM.AddNamespace("default", PROFILE_NAMESPACE_URI)  
  
        ' Get null count for column.  
        nullCountNode = profileOutput.SelectSingleNode(NULLCOUNT_XPATH, profileNSM)  
        nullCount = CType(nullCountNode.Value, Integer)  
  
        ' Get row count for table.  
        tableNode = profileOutput.SelectSingleNode(TABLE_XPATH, profileNSM)  
        rowCount = CType(tableNode.Attributes("RowCount").Value, Integer)  
  
        ' Compute and return null ratio.  
        nullRatio = nullCount / rowCount  
        Dts.Variables("AddressLine2NullRatio").Value = nullRatio  
  
        Dts.TaskResult = Dts.Results.Success  
  
      End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System;  
    using Microsoft.SqlServer.Dts.Runtime;  
    using System.Xml;  
  
    public class ScriptMain  
    {  
  
      private string FILENAME = "C:\\ TEMP\\DataProfile1.xml";  
      private string PROFILE_NAMESPACE_URI = "https://schemas.microsoft.com/DataDebugger/";  
      private string NULLCOUNT_XPATH = "/default:DataProfile/default:DataProfileOutput/default:Profiles" + "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:NullCount/text()";  
      private string TABLE_XPATH = "/default:DataProfile/default:DataProfileOutput/default:Profiles" + "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:Table";  
  
      public void Main()  
      {  
  
        string profileConnectionName;  
        string profilePath;  
        XmlDocument profileOutput = new XmlDocument();  
        XmlNamespaceManager profileNSM;  
        XmlNode nullCountNode;  
        int nullCount;  
        XmlNode tableNode;  
        int rowCount;  
        double nullRatio;  
  
        // Open output file.  
        profileConnectionName = Dts.Variables["ProfileConnectionName"].Value.ToString();  
        profilePath = Dts.Connections[profileConnectionName].ConnectionString;  
        profileOutput.Load(profilePath);  
        profileNSM = new XmlNamespaceManager(profileOutput.NameTable);  
        profileNSM.AddNamespace("default", PROFILE_NAMESPACE_URI);  
  
        // Get null count for column.  
        nullCountNode = profileOutput.SelectSingleNode(NULLCOUNT_XPATH, profileNSM);  
        nullCount = (int)nullCountNode.Value;  
  
        // Get row count for table.  
        tableNode = profileOutput.SelectSingleNode(TABLE_XPATH, profileNSM);  
        rowCount = (int)tableNode.Attributes["RowCount"].Value;  
  
        // Compute and return null ratio.  
        nullRatio = nullCount / rowCount;  
        Dts.Variables["AddressLine2NullRatio"].Value = nullRatio;  
  
        Dts.TaskResult = Dts.Results.Success;  
  
      }  
  
    }  
    ```  
  
    > [!NOTE]  
    >  El código de ejemplo incluido en este procedimiento muestra la forma de cargar los resultados de la tarea de generación de perfiles de datos desde un archivo. Para cargar los resultados de la tarea de generación de perfiles de datos desde una variable de paquete, vea el código de ejemplo alternativo que viene a continuación de este procedimiento.  
  
8.  Cierre el entorno de desarrollo de script y, a continuación, el Editor de la tarea Script.  
  
#### <a name="alternative-code-reading-the-profile-output-from-a-variable"></a>Código alternativo: leer los resultados del perfil desde una variable  
 El procedimiento anterior muestra cómo se carga el resultado de la tarea de generación de perfiles de datos desde un archivo. Sin embargo, un método alternativo consistiría en cargar dicho resultado desde una variable de paquete. Para cargar el resultado desde una variable, debe realizar los cambios siguientes en el código de ejemplo:  
  
-   Llame al método **LoadXml** de la clase **XmlDocument** en lugar de llamar al método **Load** .  
  
-   En el Editor de la tarea Script, agregue el nombre de la variable de paquete que contiene los resultados del perfil a la lista **ReadOnlyVariables** de la tarea.  
  
-   Pase el valor de cadena de la variable al método **LoadXML** , como se muestra en el siguiente código de ejemplo (en este ejemplo se usa "ProfileOutput" como nombre de la variable de paquete que contiene los resultados del perfil).  
  
    ```vb  
    Dim outputString As String  
    outputString = Dts.Variables("ProfileOutput").Value.ToString()  
    ...  
    profileOutput.LoadXml(outputString)  
    ```  
  
    ```csharp  
    string outputString;  
    outputString = Dts.Variables["ProfileOutput"].Value.ToString();  
    ...  
    profileOutput.LoadXml(outputString);  
    ```  
  
### <a name="configure-the-precedence-constraints"></a>Configurar las restricciones de precedencia  
 Se deben configurar las restricciones de precedencia con objeto de que controlen las bifurcaciones de nivel inferior del flujo de trabajo que se ejecutan dependiendo de los resultados de la tarea de generación de perfiles de datos.  
  
##### <a name="to-configure-the-precedence-constraints"></a>Para configurar las restricciones de precedencia  
  
-   En las restricciones de precedencia que conectan la tarea Script a las bifurcaciones de nivel inferior del flujo de trabajo, escriba expresiones que usen los valores de las variables para dirigir el flujo de trabajo.  
  
     Por ejemplo, puede establecer el valor de la lista **Operación de evaluación** para la restricción de precedencia en **Expresión y restricción**. A continuación, puede usar `@AddressLine2NullRatio < .90` como valor de la expresión. Esto hará que el flujo de trabajo siga la ruta seleccionada cuando las tareas previas se ejecuten correctamente, y cuando el porcentaje de valores NULL en la columna seleccionada sea inferior al 90%.  
  
## <a name="connecting-the-data-profiling-task-to-transformed-data-from-the-data-flow"></a>Conectar la tarea de generación de perfiles de datos a los datos transformados del flujo de datos  
 En lugar de generar perfiles para los datos directamente desde un origen de datos, puede generar dichos perfiles para los datos ya cargados y transformados en el flujo de datos. Sin embargo, la tarea de generación de perfiles de datos solo funciona con datos persistentes, no con datos almacenados en la memoria. Por lo tanto, primero debe usar un componente de destino para guardar los datos transformados en una tabla de ensayo.  
  
> [!NOTE]  
>  Al configurar la tarea de generación de perfiles de datos, debe seleccionar tablas y columnas existentes. Por consiguiente, debe crear la tabla de ensayo en tiempo de diseño antes de configurar la tarea. En otras palabras, este escenario no permite utilizar una tabla temporal creada en tiempo de ejecución.  
  
 Después de guardar los datos en una tabla de ensayo, puede realizar las acciones siguientes:  
  
-   Usar la tarea de generación de perfiles de datos para generar perfiles de los datos.  
  
-   Usar una tarea Script para leer los resultados, tal como se ha indicado anteriormente en este tema.  
  
-   Usar estos resultados para dirigir el flujo de trabajo posterior del paquete.  
  
 El procedimiento siguiente proporciona el método general para usar la tarea de generación de perfiles de datos con objeto de generar perfiles de los datos transformados por el flujo de datos. Muchos de estos pasos son similares a los descritos anteriormente para la generación de perfiles de datos que proceden directamente de un origen de datos externo. Conviene revisar dichos pasos para obtener más información sobre cómo configurar los distintos componentes.  
  
#### <a name="to-use-the-data-profiling-task-in-the-data-flow"></a>Para usar la tarea de generación de perfiles de datos en el flujo de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], cree un paquete.  
  
2.  En el flujo de datos, agregue, configure y conecte los orígenes y transformaciones apropiados.  
  
3.  En el flujo de datos, agregue, configure y conecte un componente de destino que guarde los datos transformados en una tabla de ensayo.  
  
4.  En el flujo de control, agregue y configure una tarea de generación de perfiles de datos que calcule los perfiles deseados a partir de los datos transformados de la tabla de ensayo. Conecte dicha tarea a la tarea Flujo de datos.  
  
5.  Configure las variables de paquete que van a contener los valores que desea recuperar de los resultados del perfil.  
  
6.  Agregue y configure una tarea Script. Conecte dicha tarea a la tarea de generación de perfiles de datos. En la tarea Script, escriba el código necesario para leer los valores deseados del resultado de la tarea de generación de perfiles de datos y rellenar las variables de paquete.  
  
7.  En las restricciones de precedencia que conectan la tarea Script a las bifurcaciones de nivel inferior del flujo de trabajo, escriba expresiones que usen los valores de las variables para dirigir el flujo de trabajo.  
  
## <a name="see-also"></a>Consulte también  
 [Configuración de la Tarea de generación de perfiles de datos](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)   
 [Visor de perfil de datos](../../integration-services/control-flow/data-profile-viewer.md)  
  
  

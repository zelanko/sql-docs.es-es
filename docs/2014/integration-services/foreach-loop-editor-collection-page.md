---
title: Editor de bucles foreach (página colección) | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.foreachloopcontainer.collection.f1
ms.assetid: 95a19dde-61ca-4d9b-aa3d-131fa4264296
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 36e2c705382d553c9833776badfacd32aed7f6d6
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85425522"
---
# <a name="foreach-loop-editor-collection-page"></a>Editor de bucles Foreach (página Colección)
  Use la página **Colección** del cuadro de diálogo **Editor de bucles Foreach** para especificar el tipo de enumerador y configurarlo.  
  
 Para más información sobre el contenedor de bucles Foreach y cómo configurarlo, vea [Contenedor de bucles Foreach](control-flow/foreach-loop-container.md) y [Configurar un contenedor de bucles Foreach](../../2014/integration-services/configure-a-foreach-loop-container.md).  
  
## <a name="static-options"></a>Opciones estáticas  
 **Avanzó**  
 Seleccione el tipo de enumerador de la lista. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Enumerador de archivos para Foreach**|Enumera archivos. Si selecciona este valor se muestran las opciones dinámicas en la sección **Enumerador de archivos para Foreach**.|  
|**Enumerador de elementos para Foreach**|Enumera los valores de un elemento. Si selecciona este valor se muestran las opciones dinámicas en la sección **Enumerador de elementos para Foreach**.|  
|**Enumerador de ADO para Foreach**|Enumera tablas o filas de las tablas. Si selecciona este valor se muestran las opciones dinámicas en la sección **Enumerador de ADO para Foreach**.|  
|**Enumerador de conjunto de filas del esquema para Foreach de ADO.NET**|Enumera un esquema. Si selecciona este valor se muestran las opciones dinámicas en la sección **Enumerador de conjunto de filas del esquema para Foreach de ADO.NET**.|  
|**Enumerador de variable para Foreach**|Enumera el valor en una variable. Si selecciona este valor, se muestran las opciones dinámicas en la sección **Enumerador de variable para Foreach**.|  
|**Enumerador de lista de nodos para Foreach**|Enumera los nodos de un documento XML. Si selecciona este valor, se muestran las opciones dinámicas en la sección **Enumerador de lista de nodos para Foreach**.|  
|**Enumerador de SMO para Foreach**|Enumera un objeto SMO. Si selecciona este valor, se muestran las opciones dinámicas en la sección **Enumerador de SMO para Foreach**.|  
|**Enumerador de blob de Azure para Foreach**|Enumerar archivos blob en la ubicación de blob especificada. Si selecciona este valor, se muestran las opciones dinámicas en la sección **Enumerador de blob de Azure para Foreach**.|  
|**Enumerador de archivos de ADLS para Para cada uno**|Enumerar archivos en ADLS con filtros. Si selecciona este valor, se muestran las opciones dinámicas en la sección **Enumerador de archivos ADLS para Para cada uno**.|
  
 **Expresiones**  
 Haga clic en **Expresiones** o expándalo para ver la lista de expresiones de propiedad existentes. Haga clic en el botón de puntos suspensivos **(…)** para agregar una expresión de propiedad para una propiedad de enumerador, o bien para editar y evaluar una expresión de propiedad existente.  
  
 **Temas relacionados:**  [Expresiones de Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md), [Editor de expresiones de propiedad](expressions/property-expressions-editor.md), [Generador de expresiones](expressions/expression-builder.md).  
  
## <a name="enumerator-dynamic-options"></a>Opciones dinámicas de los enumeradores  
  
### <a name="enumerator--foreach-file-enumerator"></a>Enumerador = Enumerador de archivos para Foreach  
 El enumerador de archivos para Foreach se utiliza para enumerar los archivos de una carpeta. Por ejemplo, si el bucle Foreach incluye una tarea Ejecutar SQL, puede utilizar el enumerador de archivos para Foreach para enumerar los archivos que contienen instrucciones SQL que ejecuta la tarea Ejecutar SQL. El enumerador puede configurarse para incluir subcarpetas.  
  
 El contenido de las carpetas y subcarpetas que enumera el enumerador de archivos para Foreach puede cambiar mientras el bucle se ejecuta ya que los procesos externos o las tareas del bucle agregan, cambian el nombre o eliminan archivos mientras el bucle se ejecuta. Esto significa que se pueden producir diversas situaciones inesperadas:  
  
-   Si los archivos se eliminan, una tarea del bucle Foreach puede realizar el trabajo en un conjunto de archivos diferente de los archivos utilizados por las tareas posteriores.  
  
-   Si los archivos se cambian de nombre y un proceso externo agrega archivos automáticamente para sustituir los archivos cuyo nombre ha cambiado, el bucle Foreach puede realizar el trabajo dos veces en el mismo contenido de archivo.  
  
-   Si se agregan archivos, puede resultar difícil determinar los archivos para los que el bucle Foreach ha realizado el trabajo.  
  
 **Carpeta**  
 Permite especificar la ruta de la carpeta raíz que se va a enumerar.  
  
 **Examinar**  
 Permite buscar la carpeta raíz.  
  
 **Archivos**  
 Permite especificar los archivos que se van a enumerar.  
  
> [!NOTE]  
>  Use caracteres comodín (*) para especificar los archivos que desea incluir en la colección. Por ejemplo, para incluir los archivos con nombres que contienen “abc”, use el filtro siguiente: \*abc\*.  
>   
>  Cuando se especifica una extensión de nombre de archivo, el enumerador también devuelve archivos que tienen la misma extensión con caracteres adicionales anexados. (Este comportamiento es el mismo que el del comando **dir** en el sistema operativo, que también compara nombres de archivo con formato 8.3 para mantener la compatibilidad con versiones anteriores). Este comportamiento del enumerador podría producir resultados inesperados. Por ejemplo, suponga que desea enumerar solo archivos de Excel 2003 y especifica "* .xls". Sin embargo, el enumerador también devolverá archivos de Excel 2007 porque esos archivos tienen la extensión, ".xlsx".  
>   
>  Puede usar una expresión para especificar los archivos que se van a incluir en una colección; para ello, expanda **expresiones** en la página **colección** , seleccione la propiedad **FileSpec** y, a continuación, haga clic en el botón de puntos suspensivos (...) para agregar la expresión de propiedad. Para obtener más información acerca de cómo seleccionar dinámicamente los archivos especificados, vea [SSIS-establecer dinámicamente la máscara de archivo: FileSpec](https://rajsudeep.blogspot.com/2010/09/ssisdynamically-set-file-mask-filespec.html)  
  
 **Completo**  
 Seleccione esta opción si desea recuperar la ruta completa de los nombres de archivo. Si se especifican caracteres comodín en la opción Archivos, las rutas completas devueltas coinciden con el filtro.  
  
 **Solo nombre**  
 Seleccione esta opción si desea recuperar únicamente los nombres. Si se especifican caracteres comodín en la opción Archivos, los nombres de archivo devueltos coinciden con el filtro.  
  
 **Nombre y extensión**  
 Seleccione esta opción si desea recuperar los nombres y las extensiones de archivo asociadas. Si se especifican caracteres comodín en la opción Archivos, el nombre y extensión de los archivos devueltos coinciden con el filtro.  
  
 **Recorrer subcarpetas**  
 Seleccione esta opción si desea incluir las subcarpetas en la enumeración.  
  
### <a name="enumerator--foreach-item-enumerator"></a>Enumerador = Enumerador de elementos para Foreach  
 El enumerador de elementos para Foreach se utiliza para enumerar los elementos de una colección. Los elementos de la colección se definen especificando las columnas y los valores de las columnas. Las columnas de una fila definen un elemento. Por ejemplo, un elemento que especifica los ejecutables que ejecuta una tarea Ejecutar proceso y el directorio de trabajo que utiliza la tarea tiene dos columnas, una que enumera los nombres de los ejecutables y otra que indica el directorio de trabajo. El número de filas determina el número de veces que se repite el bucle. Si la tabla tiene 10 filas, el bucle se repetirá 10 veces.  
  
 Para actualizar las propiedades de la tarea Ejecutar proceso, se asignan variables a las columnas de elementos mediante el índice de la columna. La primera columna definida en el elemento enumerador tiene el valor de índice de 0, la segunda columna el valor 1 y así sucesivamente. Los valores de la variable se actualizan con cada repetición del bucle. Las propiedades `Executable` y `WorkingDirectory` de la tarea Ejecutar proceso se pueden actualizar mediante expresiones de propiedad que utilizan estas variables.  
  
 **Definir los elementos de la colección Foreach Item**  
 Proporcione un valor para cada columna de la tabla.  
  
> [!NOTE]  
>  Se agrega automáticamente una nueva fila a la tabla después de escribir valores en las columnas de una fila.  
  
> [!NOTE]  
>  Si los valores proporcionados no son compatibles con el tipo de datos de la columna, el texto de muestra en color rojo.  
  
 **Tipo de datos de la columna**  
 Muestra el tipo de datos de la columna activa.  
  
 **Quitar**  
 Si quiere quitar un elemento de la lista, selecciónelo y haga clic en **Quitar** .  
  
 **Columnas**  
 Haga clic para configurar el tipo de datos de las columnas del elemento.  
  
 **Temas relacionados:** [Referencia de la interfaz de usuario del cuadro de diálogo Columnas Foreach Item](../../2014/integration-services/for-each-item-columns-dialog-box-ui-reference.md)  
  
### <a name="enumerator--foreach-ado-enumerator"></a>Enumerador = Enumerador de ADO para Foreach  
 El enumerador de ADO para Foreach se utiliza para enumerar filas o tablas de un objeto ADO o ADO.NET que está almacenado en una variable. Por ejemplo, si el bucle Foreach incluye una tarea Script que escribe un conjunto de datos en una variable, puede utilizar el enumerador de ADO para Foreach para enumerar las filas del conjunto de datos. Si la variable contiene un conjunto de datos ADO.NET, el enumerador puede configurarse para enumerar filas en varias tablas o para enumerar tablas.  
  
 **Variable de origen de objeto ADO**  
 Seleccione una variable definida por el usuario en la lista o haga clic en \<**New variable...**> para crear una nueva variable.  
  
> [!NOTE]  
>  La variable debe tener el tipo de datos Object o, de lo contrario, se producirán errores.  
  
 **Temas relacionados:** [Integration Services &#40;SSIS&#41; variables](integration-services-ssis-variables.md), [Agregar variable](../../2014/integration-services/add-variable.md)  
  
 **Filas en la primera tabla**  
 Seleccione esta opción si desea enumerar solo las filas de la primera tabla.  
  
 **Filas en todas las tablas (solo en el conjunto de datos ADO.NET)**  
 Seleccione esta opción si desea enumerar las filas de todas las tablas. Esta opción solo está disponible si todos los objetos que se van a enumerar son miembros del mismo conjunto de datos ADO.NET.  
  
 **Todas las tablas (solo en el conjunto de datos ADO.NET)**  
 Seleccione esta opción si solo desea enumerar las tablas.  
  
### <a name="enumerator--foreach-adonet-schema-rowset-enumerator"></a>Enumerador = Enumerador de conjunto de filas del esquema para Foreach de ADO.NET  
 El enumerador de conjunto de filas del esquema para Foreach de ADO.NET se utiliza para enumerar un esquema para un origen de datos especificado. Por ejemplo, si el bucle Foreach incluye una tarea Ejecutar SQL, puede utilizar el enumerador de conjunto de filas del esquema para Foreach de ADO.NET para enumerar esquemas, como las columnas de la base de datos **AdventureWorks** , y la tarea Ejecutar SQL para obtener los permisos de esquema.  
  
 **Connection**  
 Seleccione un administrador de conexiones de ADO.NET en la lista o haga clic en \<**New connection...**> para crear un nuevo administrador de conexiones de ADO.net.  
  
> [!IMPORTANT]  
>  El administrador de conexiones ADO.NET debe utilizar un proveedor .NET para OLE DB. Si se conecta a SQL Server, el proveedor recomendado es [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client, que aparece enumerado en la sección **Proveedores .NET de OleDb** del cuadro de diálogo **Administrador de conexiones** .  
  
 **Temas relacionados:** [ADO Connection Manager](connection-manager/ado-connection-manager.md), [Configure ADO.NET Connection Manager](configure-ado-net-connection-manager.md)  
  
 **Esquema**  
 Seleccione el esquema que desea enumerar.  
  
 **Establecer restricciones**  
 Permite establecer las restricciones que se deben aplicar al esquema especificado.  
  
 **Temas relacionados:** [Restricciones de esquema, cuadro de diálogo](../../2014/integration-services/schema-restrictions-dialog-box.md)  
  
### <a name="enumerator--foreach-from-variable-enumerator"></a>Enumerador = Enumerador de variable para Foreach  
 El enumerador de variable para Foreach se utiliza para enumerar los objetos enumerables incluidos en una variable especificada. Por ejemplo, si el bucle Foreach incluye una tarea Ejecutar SQL que ejecuta una consulta y almacena el resultado en una variable, puede utilizar el enumerador de variable para Foreach para enumerar los resultados de la consulta.  
  
 **Variable**  
 Seleccione una variable de la lista o haga clic \<**New variable...**> para crear una nueva variable.  
  
 **Temas relacionados:** [Integration Services &#40;SSIS&#41; variables](integration-services-ssis-variables.md), [Agregar variable](../../2014/integration-services/add-variable.md)  
  
### <a name="enumerator--foreach-nodelist-enumerator"></a>Enumerador = Enumerador de lista de nodos para Foreach  
 El enumerador de lista de nodos para Foreach se utiliza para enumerar el conjunto de nodos XML que resultan de aplicar una expresión XPath a un archivo XML. Por ejemplo, si el bucle Foreach incluye una tarea Script, puede utilizar el enumerador de lista de nodos para Foreach para pasar un valor que coincida con los criterios de la expresión XPath del archivo XML a la tarea Script.  
  
 La expresión XPath que se aplica al archivo XML es la operación XPath externa, almacenada en la propiedad OuterXPathString. Si el tipo de enumeración de XPath está establecido en `ElementCollection` , el enumerador de lista de nodos para foreach puede aplicar una expresión XPath interna, almacenada en la propiedad InnerXPathString, a una colección de elementos.  
  
 Para obtener más información acerca de cómo trabajar con datos y documentos XML, vea el artículo sobre el[uso de XML en .NET Framework](https://go.microsoft.com/fwlink/?LinkId=56214)en MSDN Library.  
  
 **DocumentSourceType**  
 Seleccione el tipo de origen del documento XML. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Entrada directa**|Establezca el origen para un documento XML.|  
|**Conexión de archivos**|Seleccione el archivo que contiene el documento XML.|  
|**Variable**|Establezca el origen para la variable que contiene el documento XML.|  
  
 **DocumentSource**  
 Si **DocumentSourceType** está establecido en **entrada directa**, proporcione el código XML o haga clic en el botón de puntos suspensivos (...) para proporcionar XML mediante el cuadro de diálogo **Editor de origen del documento**.  
  
 Si **DocumentSourceType** está establecido en **conexión de archivos**, seleccione un administrador de conexiones de archivos o haga clic en \<**New connection...**> para crear un nuevo administrador de conexiones.  
  
 **Temas relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Si **DocumentSourceType** está establecido en **variable**, seleccione una variable existente o haga clic en \<**New variable...**> para crear una nueva variable.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), [Agregar variable](../../2014/integration-services/add-variable.md).  
  
 **EnumerationType**  
 Seleccione un tipo de enumeración de la lista. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Navigator**|Se enumera mediante un objeto XPathNavigator.|  
|**Node**|Se enumeran los nodos devueltos por una operación XPath.|  
|**NodeText**|Se enumeran los nodos de texto devueltos por una operación XPath.|  
|`ElementCollection`|Se enumeran los nodos de elemento devueltos por una operación XPath.|  
  
 **OuterXPathStringSourceType**  
 Seleccione el tipo de origen de la cadena XPath. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Entrada directa**|Establezca el origen para un documento XML.|  
|**Conexión de archivos**|Seleccione el archivo que contiene el documento XML.|  
|**Variable**|Establezca el origen para la variable que contiene el documento XML.|  
  
 `OuterXPathString`  
 Si **OuterXPathStringSourceType** está establecido en **Entrada directa**, debe proporcionar la cadena XPath.  
  
 Si **OuterXPathStringSourceType** está establecido en **conexión de archivos**, seleccione un administrador de conexiones de archivos o haga clic en \<**New connection...**> para crear un nuevo administrador de conexiones.  
  
 **Temas relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Si **OuterXPathStringSourceType** está establecido en **variable**, seleccione una variable existente o haga clic en \<**New variable...**> para crear una nueva variable.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), [Agregar variable](../../2014/integration-services/add-variable.md).  
  
 **InnerElementType**  
 Si **EnumerationType** está establecido en `ElementCollection` , seleccione el tipo de elemento interno de la lista.  
  
 **InnerXPathStringSourceType**  
 Seleccione el tipo de origen de la cadena XPath interna. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Entrada directa**|Establezca el origen para un documento XML.|  
|**Conexión de archivos**|Seleccione el archivo que contiene el documento XML.|  
|**Variable**|Establezca el origen para la variable que contiene el documento XML.|  
  
 `InnerXPathString`  
 Si **InnerXPathStringSourceType** está establecido en **Entrada directa**, debe proporcionar la cadena XPath.  
  
 Si **InnerXPathStringSourceType** está establecido en **conexión de archivos**, seleccione un administrador de conexiones de archivos o haga clic en \<**New connection...**> para crear un nuevo administrador de conexiones.  
  
 **Temas relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Si **InnerXPathStringSourceType** está establecido en **variable**, seleccione una variable existente o haga clic en \<**New variable...**> para crear una nueva variable.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), [Agregar variable](../../2014/integration-services/add-variable.md).  
  
### <a name="enumerator--foreach-smo-enumerator"></a>Enumerador = Enumerador de SMO para Foreach  
 El enumerador de SMO para Foreach se utiliza para enumerar objetos de Objetos de administración de SQL Server (SMO). Por ejemplo, si el bucle Foreach incluye una tarea Ejecutar SQL, puede utilizar el enumerador de SMO para Foreach para enumerar las tablas de la base de datos **AdventureWorks** y ejecutar las consultas que realizan el recuento de filas de cada tabla.  
  
 **Connection**  
 Seleccione un administrador de conexiones de ADO.NET existente o haga clic en \<**New connection...**> para crear un nuevo administrador de conexiones.  
  
 Temas relacionados: [ADO.NET Connection Manager](connection-manager/ado-net-connection-manager.md), [Configure ADO.NET Connection Manager](configure-ado-net-connection-manager.md)  
  
 **Enumerar**  
 Especifique el objeto SMO que desea enumerar.  
  
 **Examinar**  
 Seleccione la enumeración SMO.  
  
 **Temas relacionados:** [Seleccionar enumeración de SMO, cuadro de diálogo](../../2014/integration-services/select-smo-enumeration-dialog-box.md).  
  
### <a name="enumerator--foreach-azure-blob-enumerator"></a>Enumerador = Enumerador de blob de Azure para Foreach  
 El  **Enumerador de blob de Azure**habilita un paquete SSIS para enumerar los archivos de blob en la ubicación de blob especificada. El nombre de un archivo blob enumerado se puede almacenar en una variable y usar en tareas en el Contenedor de bucles Foreach.  
  
 **Administrador de conexiones de almacenamiento de Azure**  
 Seleccione un administrador de conexiones de almacenamiento de Azure existente o cree uno que haga referencia a una cuenta de almacenamiento de Azure.  
  
 Temas relacionados: [Azure Storage Connection Manager](connection-manager/azure-storage-connection-manager.md).  
  
 **Nombre del contenedor de blob**  
 Especifique el nombre del contenedor de blob que contiene los archivos de blob que hay que enumerar.  
  
 **Directorio de blob**  
 Especifique el directorio de blob que contiene los archivos de blob que hay que enumerar. El directorio de blobs es una estructura jerárquica virtual.  
  
 **Filtro de nombre de blob**  
 Especifique un nombre de filtro para enumerar los archivos con un determinado patrón de nombre. Por ejemplo, MiHoja*.xls\* incluirá archivos como MiHoja001.xls y MiHojaABC.xlsx.  
  
 **Intervalo de tiempo de blob del filtro desde/hasta**  
 Especifique un filtro de intervalo de tiempo. Se enumerarán los archivos modificados después de **TimeRangeFrom** y antes de **TimeRangeTo** .  
### <a name="enumerator--foreach-adls-file-enumerator"></a> Enumerador = Enumerador de archivos de ADLS para Para cada uno  
El **enumerador de archivos ADLS** habilita un paquete SSIS para enumerar los archivos de ADLS con filtros. La `/` ruta de acceso completa de la barra diagonal () de los archivos enumerados se puede almacenar en una variable y usar en tareas dentro del contenedor de bucles foreach.
  
**AzureDataLakeConnection**  
Especifica un administrador de conexiones de Azure Data Lake, o crea uno nuevo que hace referencia a una cuenta de ADLS.   
  
**AzureDataLakeDirectory**  
Especifica el directorio de ADLS en el que se va a buscar.
  
**FileNamePattern**  
Especifica un filtro de nombre de archivo. Solo se enumerarán los archivos cuyo nombre coincida con el patrón especificado. Se admite el uso de los caracteres comodín `*` y `?`. 
  
**SearchRecursively**  
Especifica si se debe buscar de forma recursiva en el directorio especificado.  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Entrada de blog, sobre [SSIS para cada enumerador de lista de nodo](https://go.microsoft.com/fwlink/?LinkId=220671), en bidn.com.  
  
-   Entrada de blog, [SSIS-establecer dinámicamente la máscara de archivo: FileSpec](https://rajsudeep.blogspot.com/2010/09/ssisdynamically-set-file-mask-filespec.html).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de bucles foreach &#40;página general&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor de bucles foreach &#40;página asignaciones de variables&#41;](../../2014/integration-services/foreach-loop-editor-variable-mappings-page.md)   
 [Página expresiones](expressions/expressions-page.md)   
 [Contenedor de bucles For](control-flow/for-loop-container.md)  
  
  

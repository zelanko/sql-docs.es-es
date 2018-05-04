---
title: AMO otras clases y métodos | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: amo
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9923daa4b7cb9b504fde047f073579279b3d05e8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="amo-other-classes-and-methods"></a>Otras clases y métodos de AMO
  Esta sección contiene clases comunes que no son específicas de OLAP o de minería de datos, y que son útiles cuando se administran objetos en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Estas clases incluyen características como procedimientos almacenados, seguimientos, excepciones y copias de seguridad y restauración.  
  
 Este tema contiene las siguientes secciones:  
  
-   [Objetos de ensamblado](#Assembly)  
  
-   [Métodos de restauración y copia de seguridad](#Backup)  
  
-   [Objetos de seguimiento](#Traces)  
  
-   [Clase CaptureLog y atributo CaptureXML](#CaptureLog)  
  
-   [Clase de excepción AMOException](#AMO)  
  
 La ilustración siguiente muestra la relación de las clases que se explican en este tema.  
  
 ![Otras clases de AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-otherclasses.gif "otras clases de AMO")  
  
##  <a name="Assembly"></a> Objetos de ensamblado  
 Para crear un objeto <xref:Microsoft.AnalysisServices.Assembly>, éste se agrega a la colección de ensamblados del servidor y el objeto <xref:Microsoft.AnalysisServices.Assembly> se actualiza en el servidor mediante el método Update.  
  
 Para quitar un objeto <xref:Microsoft.AnalysisServices.Assembly>, éste se tiene que quitar mediante el método Drop del objeto <xref:Microsoft.AnalysisServices.Assembly>. Al quitar un objeto <xref:Microsoft.AnalysisServices.Assembly> de la colección de ensamblados de la base de datos, no se quita el ensamblado, únicamente le impide verlo en su aplicación hasta que vuelva a ejecutarla.  
  
 Para obtener más información sobre los métodos y propiedades disponibles, vea <xref:Microsoft.AnalysisServices.Assembly> en <xref:Microsoft.AnalysisServices> .  
  
> [!IMPORTANT]  
>  Los ensamblados COM pueden suponer un riesgo para la seguridad. Debido a esto y a otras consideraciones, los ensamblados COM están en desuso en [!INCLUDE[ssASversion10](../../../includes/ssasversion10-md.md)]. Es posible que este tipo de ensamblados no esté disponible en versiones futuras.  
  
##  <a name="Backup"></a> Métodos de restauración y copia de seguridad  
 Las copias de seguridad y restauración son métodos que se usan para realizar copias de una base de datos [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y recuperar la base de datos a partir de la copia. El método de copias de seguridad pertenece al objeto <xref:Microsoft.AnalysisServices.Database> y el método de restauración pertenece al objeto <xref:Microsoft.AnalysisServices.Server>.  
  
 Los administradores del servidor y bases de datos son los únicos que pueden realizar una copia de seguridad de una base de datos. Los administradores del servidor son los únicos que pueden restaurar una base de datos en un servidor distinto del servidor en el que se realizó la copia de seguridad. Los administradores de bases de datos pueden restaurar una base de datos sobrescribiendo la base de datos existente solo si son propietarios de la base de datos que se va a sobrescribir. Después de una restauración, puede que el administrador de bases de datos pierda el acceso a la base de datos restaurada si se restauró con sus definiciones de seguridad originales.  
  
 Los archivos de copia de seguridad de la base de datos deben tener extensiones .abf.  
  
### <a name="backup-method"></a>Método de copias de seguridad  
 Para realizar una copia de seguridad de una base de datos, use el método de copias de seguridad del objeto de la base de datos con el nombre del archivo de copia de seguridad como un parámetro.  
  
##### <a name="default-values"></a>Valores predeterminados:  
 AllowOverwrite =**false**  
  
 BackupRemotePartitions=**false**  
  
 Seguridad =**CopyAll**  
  
 ApplyCompression=**true**  
  
### <a name="restore-method"></a>Método de restauración  
 Para restaurar una base de datos a un servidor, use el método de restauración del servidor con el archivo de copia de seguridad como un parámetro.  
  
##### <a name="default-values"></a>Valores predeterminados:  
 AllowOverwrite =**false**  
  
 DataSourceType=**Remote**  
  
 Seguridad =**CopyAll**  
  
##### <a name="restrictions"></a>Restricciones  
  
1.  Una partición local no se puede restaurar como una partición remota.  
  
2.  Una partición remota no se puede restaurar como una partición local, pero una partición remota se puede restaurar en un servidor distinto del servidor en el que se realizó la copia de seguridad.  
  
### <a name="common-parameters-and-properties-for-backup-and-restore-methods"></a>Parámetros comunes y propiedades para los métodos de copias de seguridad y restauración  
  
-   **Archivo** es el nombre del archivo que se copia de seguridad (nombre UNC) desde y hacia.  
  
-   **Ubicación** especifica información de copia de seguridad específica del servidor, como **BackupFile**. Esto le permite especificar un archivo de copia de seguridad independiente para una base de datos remota.  
  
-   **DatasourceID** especifica el identificador de la base de datos subordinada en un servidor remoto.  
  
-   **ConnectionString** le permite ajustar el origen de datos remoto en caso de que el servidor remoto ha cambiado. DataSourceID siempre debe especificarse en el caso de que esté presente ConnectionString.  
  
-   **Carpeta** permite la reasignación de las carpetas para las particiones en el disco duro local  
  
-   **Original** es la carpeta original para las particiones locales.  
  
-   **Nueva** es la nueva ubicación para particiones locales que residían en la carpeta anterior 'Original' correspondiente.  
  
-   **Contraseña**, si no están en blanco, especifica que el servidor cifrará el archivo de copia de seguridad.  
  
##  <a name="Traces"></a> Objetos de seguimiento  
 El seguimiento es un marco que se usa para supervisar, reproducir y administrar una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Una aplicación cliente, como [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)], suscribe a un seguimiento y el servidor devuelve los eventos de seguimiento según lo especificado en la definición de seguimiento.  
  
 Una clase de eventos describe cada evento. La clase de eventos describe el tipo de evento que se genera. En una clase de eventos, las subclases de eventos describen un nivel más concreto de clasificación. Varias columnas describen cada evento. Las columnas que describen un evento de seguimiento son coherentes para todos los eventos y siguen la estructura de Seguimiento de SQL. La información registrada en cada columna puede diferir dependiendo de la clase de eventos; es decir, se define un conjunto predefinido de columnas para cada seguimiento, pero el significado de la columna puede diferir dependiendo de la clase de eventos. Por ejemplo, la columna TextData se usa para registrar el ASSL original para todos los eventos de instrucción.  
  
 Una definición de seguimiento puede incluir una o más clases de evento para realizar un seguimiento de forma simultánea. En cada clase de eventos, se pueden agregar una o más columnas de datos a la definición de seguimiento, pero no se deben usar todas las columnas de seguimiento. El administrador de la base de datos puede decidir qué columnas disponibles se incluirán en un seguimiento. Además, se puede realizar un seguimiento de forma selectiva de las clases de evento en basado en los criterios de filtro de cualquier columna de seguimiento.  
  
 Los seguimientos se pueden iniciar y eliminar. Se pueden ejecutar varios seguimientos en cualquier un momento. Los eventos de seguimiento se pueden capturar activos o se pueden dirigir a un archivo para el posterior análisis o reproducción. [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] es la herramienta que se usa para analizar y reproducir los eventos de seguimiento de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Se permiten varias conexiones para recibir eventos del mismo seguimiento.  
  
 Los seguimientos se dividen en dos grupos: seguimientos del servidor y seguimientos de sesiones. Los seguimientos del servidor informarán de todos los eventos del servidor; los seguimientos de sesiones únicamente informarán de los eventos de la sesión actual.  
  
 Los seguimientos de la colección de seguimientos del servidor, se definen de la siguiente manera:  
  
1.  Cree un objeto <xref:Microsoft.AnalysisServices.Trace> y rellene los datos básicos, incluidos el identificador de seguimiento, el nombre, el nombre del archivo de registro, anexar o sobrescribir, etc.  
  
2.  Agregue eventos para supervisar la colección de eventos del objeto de seguimiento. Para cada evento, se agregan columnas de datos.  
  
3.  Establezca filtros para excluir filas de datos innecesarias agregándolas a la colección de filtros.  
  
4.  Inicie el seguimiento, creando el seguimiento que no inicia la recopilación de datos.  
  
5.  Detenga el seguimiento.  
  
6.  Revise el archivo de seguimiento con [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)].  
  
 Los seguimientos del objeto de sesión, se obtienen de la siguiente manera:  
  
1.  Defina funciones para controlar los eventos de seguimiento generados por SessionTrace en la aplicación. Los posibles eventos son OnEvent y Stopped.  
  
2.  Agregue sus funciones definidas al controlador de eventos.  
  
3.  Inicie el seguimiento de la sesión.  
  
4.  Realice su proceso y permita que los controladores de funciones capturen los eventos.  
  
5.  Detenga el seguimiento de sesiones.  
  
6.  Continúe con su aplicación.  
  
##  <a name="CaptureLog"></a> Clase CaptureLog y atributo CaptureXML  
 Todas las acciones que ejecuta AMO se envían al servidor como mensajes XMLA. AMO proporciona los recursos para capturar todos estos mensajes sin los encabezados SOAP. Para obtener más información, consulte [Introducción a las clases de AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md). CaptureLog es el mecanismo de AMO para generar script de objetos y operaciones; los objetos y operaciones se incluyen en el script en XMLA.  
  
 Para empezar a capturar el código XML, debe establecerse en la propiedad del objeto de servidor CaptureXML **true**. A continuación, todas las acciones que se enviarán al servidor se comenzarán a capturar en la clase CaptureLog, sin las acciones que se envían al servidor. CaptureLog se considera una clase porque tiene un método, Clear, que se usa para borrar el registro de captura.  
  
 Para leer el registro, consiga la colección de cadenas e inicie la iteración sobre las cadenas. Asimismo, puede concatenar todos los registros en una cadena mediante el método ConcatenateCaptureLog del objeto de servidor. ConcatenateCaptureLog debe tener tres parámetros, dos de los cuales son necesarios. Los parámetros necesarios son *transaccional*, de tipo booleano, y *paralelo*, de tipo booleano. Si *transaccional* está establecido en **true**, indica que se creará el archivo por lotes XML como una sola transacción en lugar de cada comando que se va a trata como una transacción independiente. Si *paralelo* está establecido en **true**, indica que se va a grabar todos los comandos del archivo por lotes para la ejecución simultánea en lugar de secuencialmente como se registraron.  
  
##  <a name="AMO"></a> Clase de excepción AMOException  
 Use la clase de excepción AMOException para detectar con facilidad las excepciones que produce AMO en su aplicación.  
  
 AMO producirá excepciones en los diferentes problemas encontrados. En la tabla siguiente se enumera el tipo de excepciones que controla AMO. Las excepciones se derivan de la clase <xref:Microsoft.AnalysisServices.AmoException>.  
  
|Excepción|Origen|Description|  
|---------------|------------|-----------------|  
|<xref:Microsoft.AnalysisServices.AmoException>|Clase base|La aplicación recibe esta excepción cuando falta un objeto primario necesario o cuando no se encuentra en una colección un elemento solicitado.|  
|<xref:Microsoft.AnalysisServices.OutOfSyncException>|Se deriva de AMOException|La aplicación recibe esta excepción cuando AMO no está sincronizado con el motor y el motor devuelve una referencia de objeto que AMO no conoce.|  
|<xref:Microsoft.AnalysisServices.OperationException>|Se deriva de AMOException|Esta es una excepción importante que las aplicaciones reciben con frecuencia. Esta excepción contiene los detalles de un error originado en el servidor, probablemente debido a una operación AMO defectuosa como Actualizar o Procesar o Quitar.|  
|<xref:Microsoft.AnalysisServices.ResponseFormatException>|Se deriva de AMOException|Esta excepción se produce cuando el motor devuelve un mensaje en un formato que AMO no entiende.|  
|<xref:Microsoft.AnalysisServices.ConnectionException>|Se deriva de AMOException|Esta excepción se produce cuando no se puede establecer una conexión (con Server.Connect) o cuando se pierde la conexión mientras AMO se comunica con el motor (por ejemplo, durante una operación Actualizar o Procesar o Quitar).|  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices>   
 [Introducción a las clases AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [Arquitectura lógica & #40; Analysis Services - datos multidimensionales & #41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de base de datos & #40; Analysis Services - datos multidimensionales & #41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  

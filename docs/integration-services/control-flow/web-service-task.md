---
title: Tarea Servicio web | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.webservicetask.f1
- sql13.dts.designer.webservicestask.general.f1
- sql13.dts.designer.webservicestask.input.f1
- sql13.dts.designer.webservicestask.output.f1
helpviewer_keywords:
- Web Service task [Integration Services]
ms.assetid: 5c7206f1-7d6a-4923-8dff-3c4912da4157
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2aa9ecc0364accdd9050cae303afb545faf394ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65727330"
---
# <a name="web-service-task"></a>Tarea Servicio web

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La tarea Servicio web ejecuta un método de servicio web. Puede usar la tarea Servicio web para los siguientes objetivos:  
  
-   Escribir en una variable los valores devueltos por un método de servicio web. Por ejemplo, puede obtener la temperatura más alta del día con un método de servicio web y luego usar ese valor para actualizar una variable que se utiliza en una expresión que establece un valor de columna.  
  
-   Escribir en un archivo los valores devueltos por un método de servicio web. Por ejemplo, se puede escribir una lista de potenciales clientes en un archivo y luego utilizar el archivo como origen de datos en un paquete que limpia los datos antes de que se escriban en una base de datos.  
  
## <a name="wsdl-file"></a>Archivo WSDL  
 La tarea Servicio web usa un administrador de conexiones HTTP para conectarse al servicio web. El administrador de conexiones HTTP se configura independientemente de la tarea Servicio web y se hace referencia a él en la tarea. El administrador de conexiones HTTP especifica la configuración de proxy del servidor, como la dirección URL del servidor, las credenciales para obtener acceso al servidor de servicios web y la duración del tiempo de espera. Para obtener más información, vea [Administrador de conexiones HTTP](../../integration-services/connection-manager/http-connection-manager.md).  
  
> [!IMPORTANT]  
>  El administrador de conexiones HTTP solo es compatible con la autenticación anónima y la autenticación básica. No es compatible con la autenticación de Windows.  
  
 El administrador de conexiones HTTP puede apuntar a un sitio web o a un archivo de Lenguaje de descripción de servicios web (WSDL). La dirección URL del administrador de conexiones HTTP que apunta a un archivo WSDL incluye el parámetro `?WSDL` ; por ejemplo, `https://MyServer/MyWebService/MyPage.asmx?WSDL`.  
  
 El archivo WSDL debe estar localmente disponible para configurar la tarea Servicio web mediante el cuadro de diálogo **Editor de la tarea Servicio web** que proporciona el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
-   Si el administrador de conexiones HTTP apunta a un sitio web, el archivo WSDL se debe copiar manualmente en un equipo local.  
  
-   Si el administrador de conexiones HTTP apunta a un archivo WSDL, el archivo se puede descargar desde el sitio web en un archivo local mediante la tarea Servicio web.  
  
 El archivo WSDL enumera los métodos que ofrece el servicio web, los parámetros de entrada que requieren los métodos, las respuestas que devuelven los métodos, y cómo comunicarse con el servicio web.  
  
 Si el método usa parámetros de entrada, la tarea Servicio web requiere valores de parámetros. Por ejemplo, un método de servicio web que recomienda el largo de los esquíes que debe comprar de acuerdo con su altura requiere que se proporcione su altura como parámetro de entrada. Los valores de parámetros se pueden proporcionar mediante cadenas que se definen en la tarea o mediante variables definidas en el ámbito de la tarea o en un contenedor principal. La ventaja de utilizar variables es que permiten actualizar dinámicamente los valores de parámetros mediante configuraciones de paquetes o scripts. Para obtener más información, vea [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) y [Configuraciones de paquetes](../../integration-services/packages/package-configurations.md).  
  
 Muchos métodos de servicio web no usan parámetros de entrada. Por ejemplo, un método de servicio web que obtiene los nombres de los presidentes nacidos en el mes en curso no requiere un parámetro de entrada porque el servicio web puede determinar localmente cuál es el mes en curso.  
  
 Los resultados del método de servicio web se pueden escribir en una variable o un archivo. El administrador de conexiones Archivo se utiliza para especificar el archivo o para proporcionar el nombre de la variable en la que se deben escribir los resultados. Para obtener más información, vea [Administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager.md) y [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="custom-logging-messages-available-on-the-web-service-task"></a>Mensajes de registro personalizados disponibles en la tarea Servicio web  
 La siguiente tabla contiene las entradas del registro personalizadas que puede habilitar para la tarea Servicio web. Para obtener más información, vea [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|**WSTaskBegin**|La tarea inició el acceso a un servicio web.|  
|**WSTaskEnd**|La tarea completó un método de servicio web.|  
|**WSTaskInfo**|Información descriptiva acerca de la tarea.|  
  
## <a name="configuration-of-the-web-service-task"></a>Configuración de la tarea Servicio web  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-web-service-task"></a>Configuración mediante programación de la tarea Servicio web  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en uno de los temas siguientes:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WebServiceTask.WebServiceTask>  
  
## <a name="web-service-task-editor-general-page"></a>Editor de la tarea Servicio web (página General)
  Use la página **General** del cuadro de diálogo **Editor de la tarea Servicio web** para especificar un administrador de conexiones de HTTP, especificar la ubicación del archivo de Lenguaje de descripción de servicios web (WSDL) que usa la tarea Servicio web, describir la tarea Servicios web y descargar el archivo WSDL.  
  
### <a name="options"></a>Opciones  
 **HTTPConnection**  
 Seleccione un administrador de conexiones de la lista, o bien haga clic en \<**Nueva conexión…** > para crear uno.  
  
> [!IMPORTANT]  
>  El administrador de conexiones HTTP solo es compatible con la autenticación anónima y la autenticación básica. No es compatible con la autenticación de Windows.  
  
 **Temas relacionados:**  [Administrador de conexiones HTTP](../../integration-services/connection-manager/http-connection-manager.md), [Editor del administrador de conexiones HTTP &#40;página Servidor&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)  
  
 **WSDLFile**  
 Escriba la ruta de acceso completa de un archivo WSDL local del equipo, o bien haga clic en el botón Examinar **(…)** y busque el archivo.  
  
 Si ya ha descargado manualmente el archivo WSDL en el equipo, seleccione este archivo. Sin embargo, si el archivo WSDL todavía no se ha descargado, siga estos pasos:  
  
-   Cree un archivo vacío que tenga la extensión ".wsdl".  
  
-   Seleccione este archivo vacío para la opción **WSDLFile** .  
  
-   Establezca el valor de **OverwriteWSDLFile** en **True** para permitir que el archivo vacío se sobrescriba con el archivo WSDL real.  
  
-   Haga clic en **Descargar WSDL** para descargar el archivo WSDL real y sobrescribir el archivo vacío.  
  
    > [!NOTE]  
    >  La opción **Descargar WSDL** no se habilita hasta que se proporciona el nombre de un archivo local existente en el cuadro **WSDLFile** .  
  
 **OverwriteWSDLFile**  
 Indica si el archivo WSDL de la tarea Servicio web se puede sobrescribir.  
  
 Si piensa descargar el archivo WSDL utilizando el botón **Descargar WSDL** , establezca este valor en **True**.  
  
 **Nombre**  
 Proporcione un nombre único para la tarea Servicio web. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Descripción**  
 Escriba una descripción de la tarea Servicio web.  
  
 **Descargar WSDL**  
 Descarga el archivo WSDL.  
  
 Este botón no se habilita hasta que se proporciona el nombre de un archivo local existente en el cuadro **WSDLFile** .  
  
## <a name="web-service-task-editor-input-page"></a>Editor de la tarea Servicio web (página Entrada)
  Use la página **Entrada** del cuadro de diálogo **Editor de la tarea Servicio web** para especificar el servicio web, el método web y los valores que se deben proporcionar como entrada para el método web. Los valores se pueden proporcionar mediante la especificación directa de cadenas o la selección de variables en la columna Valor.  
  
### <a name="options"></a>Opciones  
 **ssNoVersion**  
 Seleccione en la lista un servicio web para ejecutar el método web.  
  
 **Método**  
 Seleccione en la lista un método web para la tarea que se va a ejecutar.  
  
 **Documentación del método web**  
 Escriba una descripción del método web, o bien haga clic en el botón Examinar **(…)** y escriba una descripción en el cuadro de diálogo **Documentación del método web**.  
  
 **Nombre**  
 Muestra los nombres de las entradas del método web.  
  
 **Tipo**  
 Muestra los tipos de datos de las entradas.  
  
> [!NOTE]  
>  La tarea Servicio web solo admite parámetros de los tipos de datos siguientes: tipos primitivos tales como enteros y cadenas; matrices y secuencias de tipos primitivos, y enumeraciones.  
  
 **Variable**  
 Active las casillas para utilizar variables que proporcionen entradas.  
  
 **Value**  
 Si las casillas de Variable están activadas, seleccione las variables de la lista para proporcionar entradas; en caso contrario, escriba los valores que se usarán en las entradas.  
  
## <a name="web-service-task-editor-output-page"></a>Editor de la tarea Servicio web (página Salida)
  Use la página **Salida** del cuadro de diálogo **Editor de la tarea Servicio web** para indicar dónde desea almacenar el resultado devuelto por el método web.  
  
### <a name="static-options"></a>Opciones estáticas  
 **OutputType**  
 Seleccione el tipo de almacenamiento que desea usar para almacenar los resultados. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Conexión de archivos**|Almacene los resultados en un archivo. Si selecciona este valor, se mostrará la opción dinámica **Archivo**.|  
|**Variable**|Almacene los resultados en una variable. Si selecciona este valor, se mostrará la opción dinámica **Variable**.|  
  
### <a name="outputtype-dynamic-options"></a>Opciones dinámicas de OutputType  
  
#### <a name="outputtype--file-connection"></a>OutputType = Conexión de archivos  
 **Archivo**  
 Seleccione un administrador de conexiones de archivos de la lista, o bien haga clic en \<**Nueva conexión…** > para crear un administrador de conexiones.  
  
 **Temas relacionados:** [Administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager.md), [Editor de administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="outputtype--variable"></a>OutputType = Variable  
 **Variable**  
 Seleccione una variable de la lista, o bien haga clic en \<**Nueva variable…** > para crear una.  
  
 **Temas relacionados:**  [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Agregar variable](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="related-content"></a>Contenido relacionado  
 Vídeo [ How to: Call a Web Service by Using the Web Service Task (SQL Server Video)](https://go.microsoft.com/fwlink/?LinkId=259642) (Procedimiento para llamar a un servicio web con la tarea Servicio web [vídeo de SQL Server]), en technet.microsoft.com.  

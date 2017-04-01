---
title: "Tarea Servicio web | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.webservicetask.f1"
helpviewer_keywords: 
  - "Servicio web, tarea [Integration Services]"
ms.assetid: 5c7206f1-7d6a-4923-8dff-3c4912da4157
caps.latest.revision: 57
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 57
---
# Tarea Servicio web
  La tarea Servicio web ejecuta un método de servicio web. Puede usar la tarea Servicio web para los siguientes objetivos:  
  
-   Escribir en una variable los valores devueltos por un método de servicio web. Por ejemplo, puede obtener la temperatura más alta del día con un método de servicio web y luego usar ese valor para actualizar una variable que se utiliza en una expresión que establece un valor de columna.  
  
-   Escribir en un archivo los valores devueltos por un método de servicio web. Por ejemplo, se puede escribir una lista de potenciales clientes en un archivo y luego utilizar el archivo como origen de datos en un paquete que limpia los datos antes de que se escriban en una base de datos.  
  
## <a name="wsdl-file"></a>Archivo WSDL  
 La tarea Servicio web usa un administrador de conexiones HTTP para conectarse al servicio web. El administrador de conexiones HTTP se configura independientemente de la tarea Servicio web y se hace referencia a él en la tarea. El administrador de conexiones HTTP especifica la configuración de proxy del servidor, como la dirección URL del servidor, las credenciales para obtener acceso al servidor de servicios web y la duración del tiempo de espera. Para obtener más información, vea [Administrador de conexiones HTTP](../../integration-services/connection-manager/http-connection-manager.md).  
  
> [!IMPORTANT]  
>  El administrador de conexiones HTTP solo es compatible con la autenticación anónima y la autenticación básica. No es compatible con la autenticación de Windows.  
  
 El administrador de conexiones HTTP puede apuntar a un sitio web o a un archivo de Lenguaje de descripción de servicios web (WSDL). La dirección URL del administrador de conexiones HTTP que apunta a un archivo WSDL incluye el parámetro `?WSDL` ; por ejemplo, `http://MyServer/MyWebService/MyPage.asmx?WSDL`.  
  
 El archivo WSDL debe estar localmente disponible para configurar la tarea Servicio web mediante el cuadro de diálogo **Editor de la tarea Servicio web** que proporciona el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
-   Si el administrador de conexiones HTTP apunta a un sitio web, el archivo WSDL se debe copiar manualmente en un equipo local.  
  
-   Si el administrador de conexiones HTTP apunta a un archivo WSDL, el archivo se puede descargar desde el sitio web en un archivo local mediante la tarea Servicio web.  
  
 El archivo WSDL enumera los métodos que ofrece el servicio web, los parámetros de entrada que requieren los métodos, las respuestas que devuelven los métodos, y cómo comunicarse con el servicio web.  
  
 Si el método usa parámetros de entrada, la tarea Servicio web requiere valores de parámetros. Por ejemplo, un método de servicio web que recomienda el largo de los esquíes que debe comprar de acuerdo con su altura requiere que se proporcione su altura como parámetro de entrada. Los valores de parámetros se pueden proporcionar mediante cadenas que se definen en la tarea o mediante variables definidas en el ámbito de la tarea o en un contenedor principal. La ventaja de utilizar variables es que permiten actualizar dinámicamente los valores de parámetros mediante configuraciones de paquetes o scripts. Para obtener más información, vea [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) y [Configuraciones de paquetes](../../integration-services/packages/package-configurations.md).  
  
 Muchos métodos de servicio web no usan parámetros de entrada. Por ejemplo, un método de servicio web que obtiene los nombres de los presidentes nacidos en el mes en curso no requiere un parámetro de entrada porque el servicio web puede determinar localmente cuál es el mes en curso.  
  
 Los resultados del método de servicio web se pueden escribir en una variable o un archivo. El administrador de conexiones Archivo se utiliza para especificar el archivo o para proporcionar el nombre de la variable en la que se deben escribir los resultados. Para obtener más información, vea [Administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager.md) y [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="custom-logging-messages-available-on-the-web-service-task"></a>Mensajes de registro personalizados disponibles en la tarea Servicio web  
 La siguiente tabla contiene las entradas del registro personalizadas que puede habilitar para la tarea Servicio web. Para obtener más información, vea [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md) y [Mensajes personalizados para registro](../../integration-services/performance/custom-messages-for-logging.md).  
  
|Entrada del registro|Description|  
|---------------|-----------------|  
|**WSTaskBegin**|La tarea inició el acceso a un servicio web.|  
|**WSTaskEnd**|La tarea completó un método de servicio web.|  
|**WSTaskInfo**|Información descriptiva acerca de la tarea.|  
  
## <a name="configuration-of-the-web-service-task"></a>Configuración de la tarea Servicio web  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de la tarea Servicio web &#40;página General&#41;](../../integration-services/control-flow/web-service-task-editor-general-page.md)  
  
-   [Editor de la tarea Servicio web &#40;página Entrada&#41;](../../integration-services/control-flow/web-service-task-editor-input-page.md)  
  
-   [Editor de la tarea Servicio web &#40;página Salida&#41;](../../integration-services/control-flow/web-service-task-editor-output-page.md)  
  
-   [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## <a name="programmatic-configuration-of-the-web-service-task"></a>Configuración mediante programación de la tarea Servicio web  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en uno de los temas siguientes:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WebServiceTask.WebServiceTask>  
  
## <a name="related-content"></a>Contenido relacionado  
 Vídeo [How to: Call a Web Service by Using the Web Service Task (SQL Server Video)](http://go.microsoft.com/fwlink/?LinkId=259642)(Cómo llamar a un servicio web usando la tarea Servicio web (vídeo de SQL Server)), en technet.microsoft.com.  

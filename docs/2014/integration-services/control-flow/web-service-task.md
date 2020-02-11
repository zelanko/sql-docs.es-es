---
title: Tarea Servicio web | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.webservicetask.f1
helpviewer_keywords:
- Web Service task [Integration Services]
ms.assetid: 5c7206f1-7d6a-4923-8dff-3c4912da4157
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f21a5f938b2dcd7b90fa71ab946d2986b0633987
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62829412"
---
# <a name="web-service-task"></a>Tarea Servicio web
  La tarea Servicio web ejecuta un método de servicio web. Puede usar la tarea Servicio web para los siguientes objetivos:  
  
-   Escribir en una variable los valores devueltos por un método de servicio web. Por ejemplo, puede obtener la temperatura más alta del día con un método de servicio web y luego usar ese valor para actualizar una variable que se utiliza en una expresión que establece un valor de columna.  
  
-   Escribir en un archivo los valores devueltos por un método de servicio web. Por ejemplo, se puede escribir una lista de potenciales clientes en un archivo y luego utilizar el archivo como origen de datos en un paquete que limpia los datos antes de que se escriban en una base de datos.  
  
## <a name="wsdl-file"></a>Archivo WSDL  
 La tarea Servicio web usa un administrador de conexiones HTTP para conectarse al servicio web. El administrador de conexiones HTTP se configura independientemente de la tarea Servicio web y se hace referencia a él en la tarea. El administrador de conexiones HTTP especifica la configuración de proxy del servidor, como la dirección URL del servidor, las credenciales para obtener acceso al servidor de servicios web y la duración del tiempo de espera. Para obtener más información, vea [Administrador de conexiones HTTP](../connection-manager/http-connection-manager.md).  
  
> [!IMPORTANT]  
>  El administrador de conexiones HTTP solo es compatible con la autenticación anónima y la autenticación básica. No es compatible con la autenticación de Windows.  
  
 El administrador de conexiones HTTP puede apuntar a un sitio web o a un archivo de Lenguaje de descripción de servicios web (WSDL). La dirección URL del administrador de conexiones HTTP que apunta a un archivo WSDL incluye el parámetro `?WSDL` ; por ejemplo, `http://MyServer/MyWebService/MyPage.asmx?WSDL`.  
  
 El archivo WSDL debe estar localmente disponible para configurar la tarea Servicio web mediante el cuadro de diálogo **Editor de la tarea Servicio web** que proporciona el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
-   Si el administrador de conexiones HTTP apunta a un sitio web, el archivo WSDL se debe copiar manualmente en un equipo local.  
  
-   Si el administrador de conexiones HTTP apunta a un archivo WSDL, el archivo se puede descargar desde el sitio web en un archivo local mediante la tarea Servicio web.  
  
 El archivo WSDL enumera los métodos que ofrece el servicio web, los parámetros de entrada que requieren los métodos, las respuestas que devuelven los métodos, y cómo comunicarse con el servicio web.  
  
 Si el método usa parámetros de entrada, la tarea Servicio web requiere valores de parámetros. Por ejemplo, un método de servicio web que recomienda el largo de los esquíes que debe comprar de acuerdo con su altura requiere que se proporcione su altura como parámetro de entrada. Los valores de parámetros se pueden proporcionar mediante cadenas que se definen en la tarea o mediante variables definidas en el ámbito de la tarea o en un contenedor principal. La ventaja de utilizar variables es que permiten actualizar dinámicamente los valores de parámetros mediante configuraciones de paquetes o scripts. Para obtener más información, vea [Variables de Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md) y [Configuraciones de paquetes](../package-configurations.md).  
  
 Muchos métodos de servicio web no usan parámetros de entrada. Por ejemplo, un método de servicio web que obtiene los nombres de los presidentes nacidos en el mes en curso no requiere un parámetro de entrada porque el servicio web puede determinar localmente cuál es el mes en curso.  
  
 Los resultados del método de servicio web se pueden escribir en una variable o un archivo. El administrador de conexiones Archivo se utiliza para especificar el archivo o para proporcionar el nombre de la variable en la que se deben escribir los resultados. Para más información, vea [Administrador de conexiones de archivos](../connection-manager/file-connection-manager.md) e [Variables de Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md).  
  
## <a name="custom-logging-messages-available-on-the-web-service-task"></a>Mensajes de registro personalizados disponibles en la tarea Servicio web  
 La siguiente tabla contiene las entradas del registro personalizadas que puede habilitar para la tarea Servicio web. Para más información, vea [Registro de Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md) y [Mensajes personalizados para registro](../custom-messages-for-logging.md).  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`WSTaskBegin`|La tarea inició el acceso a un servicio web.|  
|`WSTaskEnd`|La tarea completó un método de servicio web.|  
|`WSTaskInfo`|Información descriptiva acerca de la tarea.|  
  
## <a name="configuration-of-the-web-service-task"></a>Configuración de la tarea Servicio web  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de la tarea servicio Web &#40;página general&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor de la tarea servicio Web &#40;página de entrada&#41;](../web-service-task-editor-input-page.md)  
  
-   [Editor de la tarea servicio Web &#40;página salida&#41;](../web-service-task-editor-output-page.md)  
  
-   [Página Expresiones](../expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-web-service-task"></a>Configuración mediante programación de la tarea Servicio web  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en uno de los temas siguientes:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WebServiceTask.WebServiceTask>  
  
## <a name="related-content"></a>Contenido relacionado  
 Vídeo [How to: Call a Web Service by Using the Web Service Task (SQL Server Video)](https://go.microsoft.com/fwlink/?LinkId=259642)(Cómo llamar a un servicio web usando la tarea Servicio web (vídeo de SQL Server)), en technet.microsoft.com.  
  
 [Cómo consumir el servicio Web a través del paquete SSIS](https://www.c-sharpcorner.com/article/how-to-consume-web-service-through-ssis-package/).  
  
  

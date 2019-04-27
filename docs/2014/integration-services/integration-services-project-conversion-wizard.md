---
title: Asistente para la conversión de proyectos de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.migrationwizard.f1
ms.assetid: a192b094-4d0f-4c21-b911-460ec844a49f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e8480066485cf22c48cebbba738b2c604a50b23c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767709"
---
# <a name="integration-services-project-conversion-wizard"></a>Asistente para conversión de proyectos de Integration Services
  El **Asistente para conversión de proyectos de Integration Services** convierte un proyecto al modelo de implementación de proyectos.  
  
> [!NOTE]  
>  Si el proyecto contiene uno o más orígenes de datos, se quitan los orígenes de datos cuando se completa la conversión del proyecto. Para crear una conexión a un origen de datos que se pueden compartir los paquetes en el proyecto, agregue un administrador de conexiones en el nivel de proyecto. Para obtener más información, consulte [agregar, eliminar o compartir un administrador de conexiones en un paquete](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md).  
  
 **¿Qué desea hacer?**  
  
-   [Abrir el Asistente para conversión de proyectos de Integration Services](#open_dialog)  
  
-   [Establecer las opciones de la página Buscar paquetes](#locate)  
  
-   [Establecer las opciones de la página Seleccionar paquete](#selectPackages)  
  
-   [Establecer las opciones de la página Seleccionar destino](#destination)  
  
-   [Establecer las opciones de la página Especificar propiedades del proyecto](#projectProperties)  
  
-   [Establecer las opciones de la página Actualizar la tarea Ejecutar paquete](#executePackage)  
  
-   [Establecer las opciones de la página Seleccionar configuraciones](#configurations)  
  
-   [Establecer las opciones de la página Crear parámetros](#createParameters)  
  
-   [Establecer las opciones de la página Configurar parámetros](#configureParameters)  
  
-   [Establecer las opciones en la página Revisar](#review)  
  
-   [Establecer las opciones en Realizar conversión](#conversion)  
  
##  <a name="open_dialog"></a> Abrir el Asistente para conversión de proyectos de Integration Services  
 Para abrir el asistente **Conversión de proyecto de Integration Services** , realice una de las acciones siguientes:  
  
-   Abra el proyecto en [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]y, en el Explorador de soluciones, haga clic con el botón derecho en el proyecto y seleccione **Convertir al modelo de implementación de proyectos**.  
  
-   En el Explorador de objetos de [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], haga clic con el botón derecho en el nodo **Proyectos** y seleccione **Importar paquetes**.  
  
 Dependiendo de si ejecuta el **Asistente para la conversión de proyectos de Integration Services** desde [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] o desde [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], el asistente realiza tareas de conversión diferentes. Para más información, consulte [Deploy Projects to Integration Services Server](../../2014/integration-services/deploy-projects-to-integration-services-server.md).  
  
##  <a name="locate"></a> Establecer las opciones de la página Buscar paquetes  
  
> [!NOTE]  
>  La página **Buscar paquetes** solo está disponible cuando se ejecuta el asistente desde [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
 La siguiente opción aparece en la página al seleccionar **Sistema de archivos** en la lista desplegable **Origen** . Seleccione esta opción si el paquete reside en el sistema de archivos.  
  
 **Carpeta**  
 Escriba la ruta de acceso al paquete, o bien haga clic en **Examinar**para abrir la ubicación del paquete.  
  
 En la página se muestran las opciones siguientes al seleccionar **Almacén de paquetes SSIS** en la lista desplegable **Origen**. Para más información sobre el almacén de paquetes, vea [Administración de paquetes &#40;servicio SSIS&#41;](service/package-management-ssis-service.md).  
  
 **Server**  
 Especifique el nombre del servidor o seleccione el servidor.  
  
 **Carpeta**  
 Escriba la ruta de acceso al paquete, o bien haga clic en **Examinar**para abrir la ubicación del paquete.  
  
 En la página se muestran las opciones siguientes al seleccionar **Microsoft SQL Server** en la lista desplegable **Origen** . Seleccione esta opción si el paquete reside en Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **Server**  
 Especifique el nombre del servidor o seleccione el servidor.  
  
 **Usar la autenticación de Windows**  
 El modo de autenticación de Microsoft Windows permite que un usuario pueda conectarse a través de una cuenta de usuario de Windows. Si utiliza la autenticación de Windows, no será necesario que proporcione un nombre de usuario o una contraseña.  
  
 **Utilizar autenticación de SQL Server**  
 Cuando un usuario se conecta con un nombre de inicio de sesión y una contraseña especificados desde una conexión que no es de confianza, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] autentica la conexión (para hacerlo, comprueba si se ha configurado una cuenta de inicio de sesión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y si la contraseña especificada coincide con la almacenada anteriormente). Si [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no tiene configurada una cuenta de inicio de sesión, la autenticación no se realizará correctamente y el usuario recibirá un mensaje de error.  
  
 **Nombre de usuario.**  
 Especifique un nombre de usuario cuando utilice la autenticación de SQL Server.  
  
 **Contraseña**  
 Especifique la contraseña cuando use la autenticación de SQL Server.  
  
 **Carpeta**  
 Escriba la ruta de acceso al paquete, o bien haga clic en **Examinar**para abrir la ubicación del paquete.  
  
##  <a name="selectPackages"></a> Establecer las opciones de la página Seleccionar paquete  
 **Nombre del paquete**  
 Muestra el archivo de paquete.  
  
 **Estado**  
 Indica si un paquete está listo para convertir el modelo de implementación de proyectos.  
  
 **de mensaje**  
 Muestra un mensaje asociado al paquete.  
  
 **Contraseña**  
 Muestra una contraseña asociada al paquete. Se oculta el texto de la contraseña.  
  
 **Aplicar a la selección**  
 Haga clic en el cuadro de texto **Contraseña** para aplicar la contraseña a los paquetes seleccionados.  
  
 **Actualizar**  
 Actualiza la lista de paquetes.  
  
##  <a name="destination"></a> Establecer las opciones de la página Seleccionar destino  
 En esta página, especifique el nombre y la ruta de un nuevo archivo de implementación del proyecto (.ispac) o seleccione un archivo existente.  
  
> [!NOTE]  
>  La página **Seleccionar destino** solo está disponible cuando se ejecuta el asistente desde [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
 **Ruta de acceso de resultados**  
 Escriba la ruta de acceso al archivo de implementación, o bien haga clic en **Examinar**para abrir la ubicación del archivo.  
  
 **Nombre del proyecto**  
 Escriba el nombre del proyecto.  
  
 **Nivel de protección**  
 Seleccione el nivel de protección. Para más información, consulte [Access Control for Sensitive Data in Packages](security/access-control-for-sensitive-data-in-packages.md).  
  
 **Descripción del proyecto**  
 Escriba una descripción opcional para el proyecto.  
  
##  <a name="projectProperties"></a> Establecer las opciones de la página Especificar propiedades del proyecto  
  
> [!NOTE]  
>  La página **Especificar las propiedades del proyecto** solo está disponible cuando se ejecuta el asistente desde [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
 **Nombre del proyecto**  
 Muestra el nombre del proyecto.  
  
 **Nivel de protección**  
 Seleccione un nivel de protección para los paquetes que se incluyen en el proyecto. Para obtener más información acerca de los niveles de protección, vea [Access Control for Sensitive Data in Packages](security/access-control-for-sensitive-data-in-packages.md).  
  
 **Descripción del proyecto**  
 Escriba una descripción del proyecto opcional.  
  
##  <a name="executePackage"></a> Establecer las opciones de la página Actualizar la tarea Ejecutar paquete  
 Actualice las tareas Ejecutar paquete que se incluyen en los paquetes para usar una referencia basada en proyectos. Para obtener más información, vea [Execute Package Task Editor](../../2014/integration-services/execute-package-task-editor.md).  
  
 **Paquete primario**  
 Muestra el nombre del paquete que ejecuta el paquete secundario mediante la tarea Ejecutar paquete.  
  
 **Nombre de tarea**  
 Muestra el nombre de la tarea Ejecutar paquete.  
  
 **Referencia original**  
 Muestra la ruta de acceso actual del paquete secundario.  
  
 **Asignar referencia**  
 Seleccione un paquete secundario que esté almacenado en el proyecto.  
  
##  <a name="configurations"></a> Establecer las opciones de la página Seleccionar configuraciones  
 Seleccione las configuraciones del paquete que desea reemplazar por parámetros.  
  
 **Paquete**  
 Muestra el archivo de paquete.  
  
 **Tipo**  
 Muestra el tipo de configuración como, por ejemplo, un archivo de configuración XML.  
  
 **Cadena de configuración**  
 Muestra la ruta de acceso del archivo de configuración.  
  
 **Estado**  
 Muestra un mensaje de estado para la configuración. Haga clic en el mensaje para ver el mensaje de texto completo.  
  
 **Agregar configuraciones**  
 Agregue configuraciones de paquetes que se incluyan en otros proyectos a la lista de valores de configuración disponibles que desee reemplazar con parámetros. Puede seleccionar las configuraciones almacenadas en un sistema de archivos o en SQL Server.  
  
 **Actualizar**  
 Haga clic para actualizar la lista de configuraciones.  
  
 **Quite las configuraciones de todos los paquetes después de la conversión**  
 Es recomendable que quite todas las configuraciones del proyecto seleccionando esta opción.  
  
 Si no selecciona esta opción, solo se quitan las configuraciones que haya elegido reemplazar por parámetros.  
  
##  <a name="createParameters"></a> Establecer las opciones de la página Crear parámetros  
 Seleccione el nombre y el ámbito de parámetro para cada propiedad de configuración.  
  
 **Paquete**  
 Muestra el archivo de paquete.  
  
 **Nombre de parámetro**  
 Muestra el nombre de parámetro.  
  
 **Ámbito**  
 Seleccione el ámbito del parámetro, un paquete o un proyecto.  
  
##  <a name="configureParameters"></a> Establecer las opciones de la página Configurar parámetros  
 **Name**  
 Muestra el nombre de parámetro.  
  
 **Ámbito**  
 Muestra el ámbito del parámetro.  
  
 **Valor**  
 Muestra el valor del parámetro.  
  
 Haga clic en los puntos suspensivos junto al campo del valor para configurar las propiedades de parámetro.  
  
 En el cuadro de diálogo **Establecer detalles de parámetro** , puede modificar el valor del parámetro. También puede especificar si el valor del parámetro debe proporcionarse al ejecutar el paquete.  
  
 Puede modificar el valor en la página **Parámetros** del cuadro de diálogo **Configurar** de [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]; para ello, haga clic en el botón Examinar situado junto al parámetro. Aparece el cuadro de diálogo **Establecer valor de parámetro** .  
  
 El cuadro de diálogo **Establecer detalles de parámetros** también muestra el tipo de datos de parámetro y el origen del parámetro.  
  
##  <a name="review"></a> Establecer las opciones en la página Revisar  
 Use la página **Revisar** para confirmar las opciones que ha seleccionado para la conversión del proyecto.  
  
 **Anterior**  
 Haga clic aquí para cambiar una opción.  
  
 **Convertir**  
 Haga clic en esta opción para convertir el proyecto al modelo de implementación de proyectos.  
  
##  <a name="conversion"></a> Establecer las opciones en Realizar conversión  
 La página Realizar conversión muestra el estado de la conversión del proyecto.  
  
 **Acción**  
 Enumera un paso concreto de la conversión.  
  
 **Resultado**  
 Muestra el estado de cada paso de conversión. Haga clic en el mensaje de estado para obtener más información.  
  
 La conversión de proyectos no se guarda hasta que el proyecto se guarde en [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
 **Guardar informe**  
 Haga clic en esta opción para guardar un resumen de la conversión del proyecto en un archivo .xml.  
  
## <a name="see-also"></a>Vea también  
 [Deploy Projects to Integration Services Server](../../2014/integration-services/deploy-projects-to-integration-services-server.md)  
  
  

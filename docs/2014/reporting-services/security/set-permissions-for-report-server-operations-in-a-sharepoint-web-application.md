---
title: Establecer permisos para las operaciones del servidor de informes en una aplicación web de SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- SharePoint integration [Report Builder]
- security [Reporting Services], SharePoint integrated mode
- Report Builder 1.0, SharePoint integration
- model item security [Reporting Services]
ms.assetid: 9ea71f1a-ee9e-4337-95ff-d7cef79946e7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cb19f95d2dc5de8f461285d84776b80e3f9fb778
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66101552"
---
# <a name="set-permissions-for-report-server-operations-in-a-sharepoint-web-application"></a>Establecer permisos para las operaciones del servidor de informes en una aplicación web de SharePoint
  En el caso de un servidor de informes que se ejecuta en el modo integrado de SharePoint, la configuración de seguridad definida en el sitio de SharePoint determina el modo en que se ven y administran los informes, los modelos de informe y los orígenes de datos compartidos. Si usa los grupos, niveles de permiso y asignaciones de permiso predeterminados de SharePoint, puede trabajar con informes y otros documentos mediante la configuración de seguridad actual.  
  
 Si la configuración de seguridad predeterminada no proporciona el nivel de acceso deseado, puede usar la información que se ofrece en las siguientes secciones para saber qué permisos son necesarios para operaciones específicas:  
  
-   [Permisos para ver y administrar informes](#permissionReports)  
  
-   [Permisos para crear informes y usar el Generador de informes](#permissionReportBuilder)  
  
-   [Permisos para crear y administrar programaciones compartidas](#permissionSharedSchedules)  
  
-   [Permisos para crear y administrar suscripciones](#permissionSubscriptions)  
  
-   [Permisos para crear y administrar orígenes de datos compartidos y modelos de informe](#permissionDataSources)  
  
 Se exigen algunos permisos clave para completar casi cualquier operación en un sitio de SharePoint. Estos permisos no aparecen enumerados en las tablas de permisos y de tareas siguientes, pero debe incluirlos si está creando niveles de permisos personalizados:  
  
-   Examinar información de usuario  
  
-   Utilizar interfaces remotas  
  
-   Abrir  
  
-   Ver páginas de aplicaciones  
  
 Si usa niveles de permisos predefinidos no tendrá que realizar ninguna acción, puesto que los permisos anteriores ya se incluyen en Control total, Diseño, Colaborar, Lectura y Acceso limitado. No obstante, si usa niveles de permisos personalizados o edita los permisos asignados a un usuario o grupo concreto, debe agregar el permiso manualmente.  
  
 El permiso "Examinar información de usuario" permite al servidor de informes devolver información acerca del usuario que creó el elemento y el usuario que lo modificó por última vez. Sin este permiso, el servidor de informes devolverá los errores siguientes. Para las operaciones de exploración, el error es: "El servidor de informes encontró un error de SharePoint. ---> System.UnauthorizedAccessException: acceso denegado". Para las operaciones de publicación, el error es: "Los permisos concedidos al usuario "\<dominio>\\<usuario\>" son insuficientes para realizar esta operación".  
  
##  <a name="permissionReports"></a> Permisos para ver y administrar informes  
 Los permisos de definición de informes se definen mediante permisos de lista de la biblioteca que contiene el informe, pero puede establecer permisos en informes individuales si desea restringir el acceso. En la siguiente tabla se proporciona una lista de las tareas y los permisos compatibles.  
  
|Tarea|Permiso|  
|----------|----------------|  
|Ver un informe.|**Ver elementos** en la biblioteca que contiene los archivos o el informe individual.|  
|Ver un informe click-through que usa un modelo de informe como origen de datos.|**Ver elementos** en la biblioteca que contiene el informe y el modelo de informe, o en el informe y modelo individuales. Si no dispone de permisos para ver en el modelo, todavía puede abrir el informe, pero no podrá realizar ninguna notificación ad hoc en los datos.<br /><br /> Si el modelo de informe usa la seguridad de elementos de modelo, el usuario debe tener además el permiso **Enumerar permisos** en el modelo de informe.|  
|Ver instantáneas en el historial del informes.|**Editar elementos** en la biblioteca que contiene los archivos o el informe individual. Para un informe específico, puede ver todos los informes del historial de informes o ninguno. No se pueden establecer permisos para instantáneas individuales en el historial de informes.|  
|Cargar o publicar un informe en la biblioteca.|**Agregar elementos** en la biblioteca que contendrá el informe.|  
|Establecer propiedades en un informe, incluida la información de conexión de orígenes de datos, opciones de procesamiento y propiedades de parámetros.|**Editar elementos** en la biblioteca que contiene el informe o en el informe individual. También debe contar con permisos para ver en un origen de datos compartido (.rsds), para poder seleccionarlo y usarlo con el informe.|  
|Programar el procesamiento de informes.|Para poder seleccionar una programación compartida, debe tener el permiso **Abrir** en el sitio que contiene la biblioteca que incluye el informe. Para programar el procesamiento de informes o la expiración de la caché, debe tener el permiso **Editar elementos** en la biblioteca que contiene el informe o en el informe individual.|  
|Eliminar un informe.|**Eliminar elementos** en la biblioteca que contiene el informe o en el informe individual.|  
|Reemplazar la definición de informe por una nueva versión, sin que esto afecte a las propiedades, permisos, historial o suscripciones.|**Editar elementos** en la biblioteca que contiene el informe o en el informe individual.|  
|Crear instantáneas en el historial del informes.|**Agregar elementos** en la biblioteca que contiene el informe para el que está creando el historial de informes.|  
|Crear instantáneas en el historial del informes.|**Agregar elementos** en la biblioteca que contiene el informe para el que está creando el historial de informes.|  
|Eliminar instantáneas en el historial de informes y eliminar versiones específicas de las definiciones de informe que hayan sido desprotegidas y modificadas a lo largo del tiempo.|**Eliminar versiones** de la biblioteca que contiene el informe para el que está eliminando el historial de informes.|  
|Ver instantáneas en el historial de informes y ver versiones específicas de las definiciones de informe que hayan sido desprotegidas y modificadas a lo largo del tiempo.|**Ver versiones** en la biblioteca que contiene el informe.|  
  
##  <a name="permissionReportBuilder"></a> Permisos para crear informes y usar el Generador de informes  
 El Generador de informes es una herramienta de creación de informes que puede usar para crear informes ad hoc. El Generador de informes usa modelos de informe como un origen de datos para permitir la exploración ad hoc. Puede cargar un modelo en el Generador de informes para crear un informe, ejecutarlo, desplazarse por los datos del modelo y, opcionalmente, guardar el informe en una biblioteca. Los usuarios con permisos suficientes podrán abrir posteriormente el mismo informe y realizar también una exploración de datos ad hoc.  
  
> [!NOTE]  
>  El acceso al Generador de informes puede venir determinado por otros factores distintos de los permisos. Un administrador del sitio puede deshabilitar los informes ad hoc estableciendo las propiedades del servidor o limitar la disponibilidad del Generador de informes evitando agregar el tipo de contenido del Generador de informes, lo que impide a los usuarios crear nuevos informes desde el menú **Nuevo** de una biblioteca. Además, un administrador del servidor de informes puede hacer que el Generador de informes deje de estar disponible estableciendo propiedades en el servidor de informes. Si se cumple alguna de estas condiciones para el servidor, no podrá usar el Generador de informes aunque tenga los permisos necesarios.  
  
 En la siguiente tabla se proporciona una lista de tareas para crear informes y usar el Generador de informes, así como los permisos compatibles:  
  
|Tarea|Permiso|  
|----------|----------------|  
|Iniciar el Generador de informes.|No hay permisos que se usen explícitamente para controlar el acceso para usar el Generador de informes. El Generador de informes estará disponible si se configura la integración del servidor de informes y si dispone de permiso para agregar elementos a la biblioteca. Para iniciar el Generador de informes desde el menú **Nuevo** de la biblioteca, debe registrar el tipo de contenido del Generador de informes. Para obtener más información, vea [agregar tipos de contenido del servidor de informes a una biblioteca &#40;Reporting Services en el modo integrado de SharePoint&#41;](../add-reporting-services-content-types-to-a-sharepoint-library.md).|  
|Cargar un modelo o un origen de datos compartido.|**Agregar elementos** en la biblioteca que contendrá los archivos.|  
|Ver un modelo o un origen de datos compartido dependiente.|**Ver elementos** en la biblioteca que contiene los archivos.<br /><br /> Si el modelo incluye la configuración de seguridad de elementos de modelo, el usuario debe tener además el permiso **Enumerar permisos** en el modelo de informe.|  
|Generar un modelo a partir de un origen de datos compartido.|**Agregar elementos** en la biblioteca que contiene el archivo de origen de datos compartido (.rsds) a partir del cual está generando el modelo.|  
|Establecer permisos dentro de un modelo en elementos específicos del modelo.|**Administrar permisos** en el sitio que contiene la biblioteca y el archivo del modelo de informe (.smdl).|  
|Cargar un modelo en el Generador de informes.|**Editar elementos** en el archivo del modelo de informe (.smdl).|  
|Crear una definición de informe en el Generador de informes y guardar un informe en una biblioteca.|**Agregar elementos** para guardar el archivo en una biblioteca.|  
|Editar un informe en el Generador de informes.|**Editar elementos** en el archivo de definición de informe.|  
  
 Los permisos necesarios para crear y usar suscripciones y el historial de informes, así como para establecer opciones de procesamiento de informes y datos en un informe del Generador de informes, son los mismos que los permisos que se usan para realizar esas mismas acciones en archivos de definición de informes estándar.  
  
##  <a name="permissionSharedSchedules"></a> Permisos para crear y administrar programaciones compartidas  
 Las programaciones compartidas no son documentos que se almacenen en una biblioteca. Por este motivo, para crear y administrar estas programaciones se requieran permisos de sitio. No puede restringir el acceso a programaciones compartidas específicas. Cualquier programación compartida que cree estará disponible para cualquier usuario que cuente con el permiso Abrir en todo el sitio.  
  
 En la siguiente tabla se proporciona una lista de las tareas y permisos necesarios para crear, administrar y usar programaciones compartidas:  
  
|Tarea|Permiso|  
|----------|----------------|  
|Crear, modificar o eliminar una programación compartida.|**Administración del sitio web** en el sitio.|  
|Seleccionar una programación compartida para el procesamiento de suscripciones o la recuperación de datos.|**Abrir** en el sitio que contiene la biblioteca.|  
  
##  <a name="permissionSubscriptions"></a> Permisos para crear y administrar suscripciones  
 SharePoint exige una dependencia entre los permisos de suscripción y los permisos para ver. No podrá suscribirse a un informe que no tenga permiso para ver. Si concede permisos para suscribirse a un informe, se concederán automáticamente permisos para ver dicho informe.  
  
 En la siguiente tabla se proporciona una lista de las tareas y permisos necesarios para crear, administrar y usar suscripciones:  
  
|Tarea|Permiso|  
|----------|----------------|  
|Crear, modificar o eliminar una suscripción de usuario a un informe específico.|**Editar elementos** en la biblioteca que contiene el informe o en el propio informe. Ver elementos es un permiso dependiente y se incluirá en el nivel de permiso automáticamente. Los usuarios que pueden crear una suscripción también pueden crear programaciones personalizadas que ejecuten dicha suscripción.|  
|Seleccionar una programación compartida para usarla con la suscripción.|**Abrir** en el sitio que contiene la biblioteca.|  
|Crear, modificar o eliminar cualquier suscripción en todo un sitio.|**Administrar alertas** en el sitio.|  
  
##  <a name="permissionDataSources"></a> Permisos para crear y administrar orígenes de datos compartidos y modelos de informe  
 Un archivo de origen de datos compartido (.rsds) contiene información de conexión a orígenes de datos que pueden usar varios informes y modelos. En el caso de los informes estándar, el uso de un archivo .rsds para especificar información de conexión a orígenes de datos es opcional. En el caso de los informes controlados por modelos, se exige el uso de un archivo .rsds. Un modelo de informe siempre usa un archivo .rsds para conectarse a orígenes de datos externos.  
  
 Puede establecer propiedades en orígenes de datos compartidos que determinen si los usuarios individuales pueden ver o administrar orígenes de datos compartidos. Los permisos para ver o administrar un origen de datos compartido son distintos de los permisos para ver informes; puede ver un informe que use un archivo .rsds sin tener el permiso necesario para ver el propio archivo .rsds.  
  
|Tareas|Permiso|  
|-----------|----------------|  
|Crear un origen de datos compartido.|**Agregar elementos** en la biblioteca que contiene el origen de datos compartido. Puede crear nuevos orígenes de datos compartidos desde el menú Nuevo de una biblioteca. Para ello, debe registrar el tipo de contenido Origen de datos de informe en la biblioteca. Para obtener más información, vea [agregar tipos de contenido del servidor de informes a una biblioteca &#40;Reporting Services en el modo integrado de SharePoint&#41;](../add-reporting-services-content-types-to-a-sharepoint-library.md).|  
|Modificar un origen de datos compartido.|**Editar elementos** en la biblioteca que contiene el origen de datos compartido o en el propio origen de datos compartido.|  
|Eliminar un origen de datos compartido.|**Eliminar elementos** en la biblioteca que contiene el origen de datos compartido o en el propio origen de datos compartido.|  
|Usar un origen de datos compartido (.rsds) con un informe.|**Editar elementos** en el informe o en la biblioteca que contiene el informe. Seleccionar un origen de datos compartido forma parte del proceso de establecer las propiedades del origen de datos en un informe.|  
|Generar un modelo de informe a partir de un origen de datos compartido.|**Agregar elementos** en la biblioteca que contendrá el modelo de informe.|  
|Eliminar un modelo de informe.|**Eliminar elementos** en la biblioteca que contiene el modelo de informe o en el propio modelo de informe.|  
|Establecer permisos dentro de un modelo en elementos específicos del modelo.|**Administrar permisos** en el sitio que contiene la biblioteca y el archivo del modelo de informe (.smdl).|  
  
> [!NOTE]  
>  No existen permisos para modificar modelos de informe. Aunque se pueden crear o eliminar modelos de informe, no se pueden modificar desde un sitio de SharePoint. Para poder modificar modelos de informe, es necesario usar el Diseñador de modelos, una herramienta de creación de cliente a la que no afectan los permisos que haya establecido en SharePoint.  
  
## <a name="see-also"></a>Consulte también  
 [Conceder permisos sobre elementos del servidor de informes en un sitio de SharePoint](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Comparar roles y tareas de Reporting Services con grupos y permisos de SharePoint](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [Conceder permisos sobre elementos del servidor de informes en un sitio de SharePoint](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Uso de la seguridad integrada de Windows SharePoint Services para los elementos del servidor de informes](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)  
  
  

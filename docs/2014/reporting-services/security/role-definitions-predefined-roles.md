---
title: Roles predefinidos | Microsoft Docs
ms.custom: ''
ms.date: 10/22/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- security [Reporting Services], defaults
- default security
- role-based security [Reporting Services], defaults
ms.assetid: 6b46db51-7c30-467d-a251-50f50647fe21
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5567ee441075f015a7d6418761b30d29c591698f
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56035136"
---
# <a name="predefined-roles"></a>Roles predefinidos
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se instala junto con roles predefinidos que puede usar para conceder acceso a operaciones del servidor de informes. Cada rol predefinido describe una recopilación de tareas relacionadas. Puede asignar grupos y cuentas de usuario a los roles predefinidos para proporcionar acceso inmediato a las operaciones del servidor de informes.  
  
## <a name="how-to-use-predefined-roles"></a>Cómo usar los roles predefinidos  
  
1.  Revise los roles predefinidos para determinar si puede utilizarlos tal y como están. Si necesita ajustar las tareas o definir roles adicionales, conviene que lo haga antes de empezar a asignar usuarios a roles específicos.  
  
2.  Identifique qué usuarios y grupos requieren acceso al servidor de informes y en qué nivel. A la mayoría de los usuarios se les debería asignar el rol **Explorador** o el rol **Generador de informes** . A un pequeño número de usuarios se les debería asignar el rol **Publicador** . A el rol **Administrador de contenido**conviene asignar muy pocos usuarios.  
  
3.  Cuando esté preparado para asignar cuentas de usuario y de grupo a roles concretos, use el Administrador de informes. Para obtener más información, vea [Conceder a un usuario acceso a un servidor de informes &#40;Administrador de informes&#41;](grant-user-access-to-a-report-server.md)conviene asignar muy pocos usuarios.  
  
##  <a name="bkmk_rolelist"></a> Definiciones de roles predefinidos  
 Los roles predefinidos se definen de acuerdo con las tareas que admiten. Puede modificar estos roles o reemplazarlos por roles personalizados.  
  
 El*ámbito* define los límites dentro de los cuales se usan los roles. Los roles de nivel de elemento proporcionan diversos niveles de acceso a los elementos del servidor de informes y a las operaciones que afectan a esos elementos. Los roles de nivel de elemento se definen en el nodo raíz (Inicio), así como en todos los elementos de la jerarquía de carpetas del servidor de informes. Los roles de nivel de sistema autorizan el acceso en el nivel de sitio. Los roles de nivel de elemento y de nivel de sistema se excluyen mutuamente, pero se utilizan juntos para proporcionar permisos completos al contenido y a las operaciones del servidor de informes.  
  
 En la tabla siguiente se describen los roles predefinidos, su ámbito y el modo de usarlos.  
  
|Rol predefinido|ámbito|Descripción|  
|---------------------|-----------|-----------------|  
|[Rol Administrador de contenido](#bkmk_content)|Elemento|Incluye todas las tareas de nivel de elemento. Los usuarios que se asignan a este rol tienen permiso total para administrar el contenido del servidor de informes, así como capacidad para conceder permisos a otros usuarios y definir la estructura de carpetas para almacenar informes y otros elementos.|  
|[Rol Publicador](#bkmk_publisher)|Elemento|Los usuarios que se asignan a este rol pueden agregar elementos a un servidor de informes, así como crear y administrar las carpetas que contienen esos elementos.|  
|[Rol Explorador](#bkmk_browser)|Elemento|Los usuarios que se asignan a este rol pueden ejecutar informes, suscribirse a informes y navegar por la estructura de carpetas.|  
|[Rol Generador de informes](#bkmk_reportbuilder)|Elemento|Los usuarios que se asignan a este rol pueden crear y editar informes en el Generador de informes.|  
|[Rol Mis informes](#bkmk_myreports)|Elemento|Los usuarios que se asignan a este rol pueden administrar un área de trabajo personal para almacenar y utilizar informes y otros elementos.|  
|[Rol Administrador del sistema](#bkmk_systemadministrator)|Sistema|Los usuarios que se asignan a este rol pueden habilitar características y establecer valores predeterminados, establecer la seguridad de todo el sitio, crear definiciones de roles en Management Studio y administrar trabajos.|  
|[Rol Usuario del sistema](#bkmk_systemuser)|Sistema|Los usuarios que se asignan a este rol pueden ver información básica sobre el servidor de informes, como la información de programación en una programación compartida.|  
  
##  <a name="bkmk_content"></a> Rol Administrador de contenido  
 El rol **Administrador de contenido** es un rol predefinido que incluye tareas que le resultarán útiles a un usuario que administre informes y contenido web, pero que no cree necesariamente informes ni administre un servidor web o una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Un administrador de contenido implementa informes, administra modelos de informe y conexiones a orígenes de datos, y toma decisiones sobre cómo se utilizan los informes. De manera predeterminada, todas las tareas de nivel de elemento están seleccionadas para la definición del rol **Administrador de contenido** .  
  
 El rol **Administrador de contenido** se suele utilizar con el rol **Administrador del sistema** . En conjunto, las dos definiciones de roles proporcionan un conjunto completo de tareas para los usuarios que necesitan acceso completo a todos los elementos de un servidor de informes. Aunque el rol **Administrador de contenido** proporciona acceso completo a informes, modelos de informes, carpetas y otros elementos dentro de la jerarquía de carpetas, no proporciona acceso a los elementos de nivel de sitio u operaciones. Las tareas como la creación y la administración de programaciones compartidas, el establecimiento de propiedades del servidor y la administración de definiciones de rol son tareas de nivel de sistema incluidas en el rol **Administrador del sistema** . Por esta razón, recomendamos que cree una segunda asignación de rol en el nivel de sitio que proporcione acceso a las programaciones compartidas.  
  
### <a name="content-manager-tasks"></a>Tareas del Administrador de contenido  
 La siguiente tabla muestra las tareas que se incluyen en el rol **Administrador de contenido** .  
  
|Tarea|Descripción|  
|----------|-----------------|  
|Usar informes|Permite leer definiciones de informes.|  
|Crear informes vinculados|Crear informes vinculados que se basen en un informe no vinculado.|  
|Administrar todas las suscripciones|Ver, modificar y eliminar cualquier suscripción para informes e informes vinculados, independientemente de quién sea su propietario. Esta tarea también permite crear suscripciones controladas por datos.|  
|Administrar orígenes de datos|Cree y elimine elementos de orígenes de datos compartidos; vea y modifique el contenido y las propiedades de un origen de datos.|  
|Administrar carpetas|Cree, vea y elimine carpetas; vea y modifique propiedades de carpetas.|  
|Administrar modelos|Crear, ver y eliminar modelos; ver y modificar propiedades de modelos.|  
|Administrar suscripciones individuales|Crear, ver, modificar y eliminar suscripciones de usuarios a informes e informes vinculados.|  
|Administrar historial de informe|Crear, ver y eliminar el historial del informe, ver propiedades del historial del informe; ver y modificar la configuración que determina los límites del historial de instantáneas y cómo funciona el almacenamiento en caché.|  
|Administrar informes|Agregue y elimine informes, modifique parámetros de informes, vea y modifique propiedades de informes, vea y modifique orígenes de datos que proporcionen contenido al informe, vea y modifique definiciones de informe y establezca directivas de seguridad de nivel de informe.|  
|Administrar recursos|Cree, modifique y elimine recursos; vea y modifique propiedades de recursos.|  
|Establecer la seguridad de elementos individuales|Definir directivas de seguridad para informes, informes vinculados, carpetas, recursos y orígenes de datos. Para obtener más información, vea [Elementos protegibles](securable-items.md).|  
|Ver orígenes de datos|Vea elementos de orígenes de datos compartidos en la jerarquía de carpetas.|  
|Ver informes|Ejecutar informes y ver propiedades de informes.|  
|Ver modelos|Ver los modelos de la jerarquía de carpetas, utilizar modelos como orígenes de datos para un informe y ejecutar consultas en el modelo para recuperar datos.|  
|Ver recursos|Ver recursos y propiedades de recursos.|  
|Ver carpetas|Ver el contenido de carpetas y navegar por la jerarquía de carpetas.|  
  
### <a name="customizing-the-content-manager-role"></a>Personalizar el rol Administrador de contenido  
 Este rol está destinado a usuarios de confianza cuya responsabilidad general sea administrar y mantener el contenido del servidor de informes. Puede quitar tareas de esta definición, pero, al hacerlo, es posible que no quede claro qué puede administrarse. Por ejemplo, si quita la tarea "Ver informes" de esta definición de rol, impedirá que el **Administrador de contenido** pueda ver el contenido de los informes y, por lo tanto, no podrá comprobar los cambios en la configuración de credenciales y parámetros.  
  
 El rol **Administrador de contenido** se usa en la seguridad predeterminada. Para más información, vea [Using Default Security](role-definitions-predefined-roles.md).  
  
##  <a name="bkmk_publisher"></a> Rol Publicador  
 El rol **Publicador** es una definición de rol integrada que incluye tareas que permiten a los usuarios agregar contenido a un servidor de informes. Este rol ya está predefinido para mayor comodidad. Se utiliza en el momento en que se crean asignaciones de roles que la incluyan. Este rol está destinado a usuarios que crean informes o modelos en el Diseñador de informes o en el Diseñador de modelos y, después, publican estos elementos en un servidor de informes.  
  
> [!CAUTION]  
>  Solo se deben conceder permisos para publicar elementos en un servidor de informes a usuarios de confianza. El rol Publicador concede permisos muy variados, con los cuales los usuarios pueden cargar cualquier tipo de archivo en un servidor de informes. Si un informe o un archivo HTML cargado contiene script malintencionado, cualquier usuario que haga clic en el informe o documento HTML ejecutará el script con sus credenciales.  
  
 Las definiciones de informe pueden incluir script y otros elementos que son vulnerables a ataques de inyección de código HTML cuando el informe se representa en HTML en tiempo de ejecución. Si un informe publicado contiene script malintencionado, cualquier usuario que lo ejecute, sin saberlo, hará que el script se ejecute cuando se abra el informe. Si el usuario tiene permisos elevados, el script se ejecutará con esos permisos.  
  
 Para reducir el riesgo de que los usuarios ejecuten scripts malintencionados sin ser conscientes de ello, limite el número de usuarios que tienen permiso para publicar contenido y asegúrese de que los usuarios publican únicamente documentos e informes que procedan de fuentes de confianza. Si no está seguro de si una definición de informe es segura para su publicación, debe abrir el archivo .rdl en un editor de texto y buscar etiquetas de script. El script malintencionado puede estar oculto en expresiones y direcciones URL (por ejemplo, una dirección URL en una acción de navegación).  
  
### <a name="publisher-tasks"></a>Tareas de Publicador  
 La siguiente tabla muestra las tareas que se incluyen en el rol **Publicador** .  
  
|Tarea|Descripción|  
|----------|-----------------|  
|Crear informes vinculados|Cree informes vinculados y publíquelos en una carpeta del servidor de informes.|  
|Administrar orígenes de datos|Cree y elimine elementos de orígenes de datos compartidos; vea y modifique el contenido y las propiedades de un origen de datos.|  
|Administrar carpetas|Cree, vea y elimine carpetas; vea y modifique propiedades de carpetas.|  
|Administrar informes|Agregue y elimine informes, modifique parámetros de informes, vea y modifique propiedades de informes, vea y modifique orígenes de datos que proporcionen contenido al informe, vea y modifique definiciones de informe.|  
|Administrar modelos|Cree, vea y elimine modelos de informe; vea y modifique propiedades de modelos de informe.|  
|Administrar recursos|Cree, modifique y elimine recursos; vea y modifique propiedades de recursos.|  
  
### <a name="customizing-the-publisher-role"></a>Personalizar el rol Publicador  
 Puede modificar el rol **Publicador** para que se adapte a sus necesidades. Por ejemplo, puede quitar la tarea "Crear informes vinculados" si no desea que los usuarios puedan crear y publicar informes vinculados, o puede agregar la tarea "Ver carpetas" para que los usuarios puedan navegar por la jerarquía de carpetas cuando estén seleccionando la ubicación de un nuevo elemento.  
  
 Como mínimo, los usuarios que publican informes desde el Diseñador de informes necesitan la tarea "Administrar informes" para poder agregar un informe al servidor de informes. Si el usuario debe publicar informes que utilicen orígenes de datos compartidos o archivos externos, también debe incluir "Administrar orígenes de datos" y "Administrar recursos". Por otra parte, si el usuario también necesita crear una carpeta como parte del proceso de publicación, debe incluir 'Administrar carpetas'.  
  
##  <a name="bkmk_browser"></a> Rol Explorador  
 El rol **Explorador** es un rol predefinido que incluye tareas útiles para un usuario que vea informes, pero que no los cree ni administre necesariamente. Este rol proporciona capacidades básicas para el uso convencional de un servidor de informes. Sin estas tareas, a los usuarios les puede resultar difícil utilizar un servidor de informes.  
  
 El rol **Explorador** debería utilizarse con el rol **Usuario del sistema** . En conjunto, las dos definiciones de roles proporcionan un conjunto completo de tareas para los usuarios que interactúan con los elementos de un servidor de informes. Aunque el rol **Explorador** proporciona acceso de vista a informes, modelos de informes, carpetas y otros elementos dentro de la jerarquía de carpetas, no proporciona acceso a los elementos de nivel de sitio como programaciones compartidas, que son útiles cuando se crean suscripciones. Por esta razón, recomendamos que cree una segunda asignación de rol en el nivel de sitio que proporcione acceso a las programaciones compartidas.  
  
### <a name="browser-tasks"></a>Tareas del Explorador  
 La siguiente tabla muestra las tareas que se incluyen en la definición del rol **Explorador** .  
  
|Tarea|Descripción|  
|----------|-----------------|  
|Ver informes|Ejecutar un informe y ver propiedades de informe.|  
|Ver recursos|Ver recursos y propiedades de recursos.|  
|Ver carpetas|Ver el contenido de carpetas y navegar por la jerarquía de carpetas.|  
|Ver modelos|Ver los modelos de la jerarquía de carpetas, utilizar modelos como orígenes de datos para un informe y ejecutar consultas en el modelo para recuperar datos.|  
|Administrar suscripciones individuales|Crear, ver, modificar y eliminar suscripciones de usuarios a informes e informes vinculados, así como crear programaciones para dichas suscripciones.|  
  
### <a name="customizing-the-browser-role"></a>Personalizar el rol Explorador  
 Puede modificar el rol **Explorador** para que se adapte a sus necesidades. Por ejemplo, puede quitar la tarea "Administrar suscripciones individuales" si no desea permitir suscripciones o puede quitar la tarea "Ver recursos" si no desea que los usuarios vean documentación auxiliar u otros elementos que se puedan cargar en el servidor de informes.  
  
 Como mínimo, estE rol debe admitir las tareas "Ver informes" y "Ver carpetas" para permitir la visualización y la navegación por carpetas. No debería quitar la tarea "Ver carpetas" a no ser que desee eliminar la navegación por carpetas. Igualmente, no debería quitar la tarea "Ver informes" a no ser que desee impedir que los usuarios los vean. Estos tipos de modificaciones indican la necesidad de una definición de rol personalizada que se aplique selectivamente a un grupo de usuarios específico.  
  
##  <a name="bkmk_reportbuilder"></a> Rol Generador de informes  
 El rol **Generador de informes** es un rol predefinido que incluye tareas para cargar informes en el Generador de informes, y para ver la jerarquía de carpetas y navegar por ella. Para crear y modificar informes en el Generador de informes, debe tener también una asignación de roles del sistema que incluya la tarea "Ejecutar definiciones de informe", necesaria para procesar informes localmente en el Generador de informes.  
  
### <a name="report-builder-tasks"></a>Tareas del Generador de informes  
 La siguiente tabla muestra las tareas que se incluyen en la definición del rol **Generador de informes** .  
  
|Tarea|Descripción|  
|----------|-----------------|  
|Usar informes|Permite leer definiciones de informes.|  
|Ver informes|Ejecutar un informe y ver propiedades de informe.|  
|Ver recursos|Ver recursos y propiedades de recursos.|  
|Ver carpetas|Ver el contenido de carpetas y navegar por la jerarquía de carpetas.|  
|Ver modelos|Ver los modelos de la jerarquía de carpetas, utilizar modelos como orígenes de datos para un informe y ejecutar consultas en el modelo para recuperar datos.|  
|Administrar suscripciones individuales|Crear, ver, modificar y eliminar suscripciones de usuarios a informes e informes vinculados, así como crear programaciones para dichas suscripciones.|  
  
### <a name="customizing-the-report-builder-role"></a>Personalizar el rol Generador de informes  
 Puede modificar el rol **Generador de informes** para adaptarlo a sus necesidades. Las recomendaciones suelen ser iguales que para el rol **Explorador** : quite la tarea "Administrar suscripciones individuales" si no desea admitir suscripciones, quite la tarea "Ver recursos" si no desea que los usuarios vean recursos y mantenga las tareas "Ver informes" y "Ver carpetas" para permitir la visualización y navegación en carpetas.  
  
 La tarea más importante de esta definición de rol es "Usar informes", que permite a un usuario cargar una definición de informe desde el servidor de informes a una instancia local del Generador de informes. Si no desea admitir esta tarea, puede eliminar esta definición de rol y usar el rol **Explorador** para admitir el acceso general al servidor de informes.  
  
##  <a name="bkmk_myreports"></a> Rol Mis informes  
 El rol **Mis informes** es un rol predefinido que incluye un conjunto de tareas útiles para los usuarios de la característica Mis informes. Esta definición de rol incluye tareas que conceden permisos administrativos a los usuarios sobre la carpeta Mis informes de su propiedad.  
  
 Aunque puede elegir otro rol para utilizarlo con la característica Mis informes, es recomendable que elija uno que se utilice exclusivamente para la seguridad de Mis informes. Para obtener más información, vea [Proteger Mis informes](secure-my-reports.md).  
  
### <a name="my-reports-tasks"></a>Tareas de Mis informes  
 En la siguiente tabla se muestran las tareas que se incluyen en el rol **Mis informes** .  
  
|Tarea|Descripción|  
|----------|-----------------|  
|Crear informes vinculados|Cree informes vinculados que se basen en informes almacenados en la carpeta Mis informes del usuario.|  
|Administrar carpetas|Cree, vea y elimine carpetas; vea y modifique propiedades de carpetas.|  
|Administrar orígenes de datos|Cree y elimine elementos de orígenes de datos compartidos; vea y modifique el contenido y las propiedades de un origen de datos.|  
|Administrar suscripciones individuales|Cree, vea, modifique y elimine suscripciones para informes e informes vinculados.|  
|Administrar informes|Agregue y elimine informes, modifique parámetros de informes, vea y modifique propiedades de informes, vea y modifique orígenes de datos que proporcionen contenido al informe, vea y modifique definiciones de informe y establezca directivas de seguridad de nivel de informe.|  
|Administrar recursos|Cree, modifique y elimine recursos; vea y modifique propiedades de recursos.|  
|Ver informes|Ejecute informes que se almacenen en la carpeta Mis informes del usuario y vea propiedades de informes.|  
|Ver orígenes de datos|Vea elementos de orígenes de datos compartidos en la jerarquía de carpetas.|  
|Ver recursos|Ver recursos y propiedades de recursos.|  
|Ver carpetas|Vea el contenido de carpetas.|  
  
### <a name="customizing-the-my-reports-role"></a>Personalizar el rol Mis informes  
 Puede modificar este rol para que se adapte a sus necesidades. Sin embargo, se recomienda conservar las tareas "Administrar informes" y "Administrar carpetas" para permitir la administración básica del contenido. Además, este rol debería permitir todas las tareas basadas en vistas, de forma que los usuarios puedan ver el contenido de las carpetas y ejecutar los informes que administren.  
  
 Aunque la tarea 'Establecer la seguridad de elementos individuales' no forma parte de la definición predeterminada del rol, puede agregar esta tarea al rol **Mis informes** para que los usuarios puedan personalizar la configuración de seguridad de las subcarpetas e informes.  
  
##  <a name="bkmk_systemadministrator"></a> Rol Administrador del sistema  
 El rol **Administrador del sistema** es un rol predefinido que incluye tareas útiles para un administrador de servidor de informes con responsabilidad global sobre el servidor, pero no necesariamente sobre su contenido.  
  
 Para crear una asignación de roles que incluya este rol, utilice la página Configuración del sitio del Administrador de informes o utilice los comandos que aparecen al hacer clic con el botón secundario en el nodo del servidor de informes en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 El rol **Administrador del sistema** no transmite el mismo conjunto completo de permisos que un administrador local puede tener en un equipo. En lugar de ello, el rol **Administrador del sistema** incluye operaciones que se realizan en el nivel de sitio y no en el nivel de elemento. Para los usuarios que requieren acceso tanto a las operaciones de todo el sitio como a los elementos almacenados en el servidor de informes, cree una segunda asignación de roles en la carpeta Inicio que incluya el rol **Administrador de contenido** . En conjunto, las dos definiciones de roles proporcionan un conjunto completo de tareas para los usuarios que necesitan acceso completo a todos los elementos de un servidor de informes.  
  
### <a name="system-administrator-tasks"></a>Tareas de Administrador del sistema  
 La siguiente tabla muestra las tareas que se incluyen en el rol **Administrador del sistema** .  
  
|Tarea|Descripción|  
|----------|-----------------|  
|Ejecutar definiciones de informe|Inicie la ejecución de la definición del informe sin publicarlo en un servidor de informes.|  
|Administrar trabajos|Vea y cancele trabajos que se estén ejecutando. Para obtener más información, vea [Administrar un proceso en ejecución](../subscriptions/manage-a-running-process.md).|  
|Administrar propiedades del servidor de informes|Vea y modifique propiedades que se apliquen al servidor de informes y a elementos administrados por el servidor de informes.<br /><br /> Esta tarea permite cambiar el nombre del Administrador de informes, habilitar Mis informes y establecer los valores predeterminados del historial del informe.|  
|Administrar roles|Cree, vea, modifique y elimine definiciones de roles.<br /><br /> Los miembros del rol **Administrador del sistema** pueden utilizar la página Configuración del sitio para administrar roles.|  
|Administrar programaciones compartidas|Cree, vea, modifique y elimine programaciones compartidas que sirven para ejecutar o actualizar informes.|  
|Administrar la seguridad del servidor de informes|Vea y modifique asignaciones de roles del sistema.|  
  
 El rol **Administrador del sistema** se utiliza en la seguridad predeterminada. Para más información, vea [Using Default Security](role-definitions-predefined-roles.md).  
  
##  <a name="bkmk_systemuser"></a> Rol Usuario del sistema  
 El rol **Usuario del sistema** es un rol predefinido que incluye tareas que permiten a los usuarios ver información básica sobre el servidor de informes. También incluye compatibilidad para la carga de un informe en el Generador de informes. El Generador de informes es una aplicación cliente que puede procesar un informe independientemente de un servidor de informes. La tarea "Ejecutar definiciones de informe" está pensada para utilizarse con el Generador de informes. Si no utiliza el Generador de informes, puede quitar esta tarea del rol **Usuario del sistema** . La siguiente tabla muestra las tareas que se incluyen en la definición de roles **Usuario del sistema** .  
  
### <a name="system-user-tasks"></a>Tareas de Usuario del sistema  
  
|Tarea|Descripción|  
|----------|-----------------|  
|Ejecutar definiciones de informe|Ejecute un informe sin publicarlo en un servidor de informes.|  
|Ver propiedades del servidor de informes|Vea las propiedades correspondientes al servidor de informes, como el nombre de aplicación, si está habilitado Mis informes y los valores predeterminados del historial del informe.<br /><br /> Si quita esta tarea del rol **Usuario del sistema** , la página Configuración del sitio no estará disponible. Además, el título de la aplicación no aparecerá en la parte superior de todas las páginas. De forma predeterminada, el título para Administrador de informes es "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]".|  
|Ver programaciones compartidas|Vea programaciones compartidas que sirven para ejecutar o actualizar informes.<br /><br /> Si quita esta tarea del rol **Usuario del sistema** , los usuarios no podrán seleccionar programaciones compartidas para usarlas con suscripciones y otras operaciones programadas.|  
  
 El rol **Usuario del sistema** se puede utilizar para complementar la seguridad predeterminada. Puede incluir el rol en nuevas asignaciones de roles que amplíen el acceso al servidor de informes para usuarios de informes. Para obtener más información, consulte [Conceder permisos en un servidor de informes en modo nativo](granting-permissions-on-a-native-mode-report-server.md).  
  
## <a name="see-also"></a>Vea también  
 [Crear, eliminar o modificar un rol &#40;Management Studio&#41;](role-definitions-create-delete-or-modify.md)   
 [Conceder a un usuario acceso a un servidor de informes &#40;Administrador de informes&#41;](grant-user-access-to-a-report-server.md)   
 [Modificar o eliminar una asignación de roles &#40;Administrador de informes&#41;](role-assignments-modify-or-delete.md)   
 [Granting Permissions on a Native Mode Report Server](granting-permissions-on-a-native-mode-report-server.md)   
 [Tareas y permisos](tasks-and-permissions.md)  
  
  

---
title: Conceder permisos de base de datos (Analysis Services) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions [Analysis Services], full control
- full control permissions [Analysis Services]
ms.assetid: be7e5f64-af43-47d6-84a5-c5c1c277d644
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c58a338f700785bb338703c72e3b435a7aa22b94
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="grant-database-permissions-analysis-services"></a>Otorgar permisos de base de datos (Analysis Services)
  Si va a empezar a usar Analysis Services y tiene conocimientos sobre bases de datos relacionales, lo primero que necesita saber es que, en lo que respecta al acceso a datos, la base de datos no es el objeto protegible principal en Analysis Services.  
  
 La estructura de consultas primordial en Analysis Services son los cubos (o modelos tabulares), con los permisos de usuarios que se establecen en estos objetos en particular. En comparación con el motor de bases de datos relacionales, donde los inicios de sesión de base de datos y los permisos de usuario (en general, **db_datareader**) se establecen en la propia base de datos, una base de datos de Analysis Services es sobre todo un contenedor para los objetos de consulta principales de un modelo de datos. Si su objetivo inmediato es habilitar el acceso a datos para un cubo o modelo tabular, por ahora puede omitir los permisos de base de datos y pasar directamente a este tema: [Otorgar permisos para cubos o modelos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
 Los permisos de base de datos en Analysis Services habilitan las funciones administrativas; en general, como es el caso del permiso de base de datos Control total o de índole más granular si se trata de delegar operaciones de procesamiento. Los niveles de permiso para las bases de datos de Analysis Services se especifican en el panel **General** del cuadro de diálogo **Crear rol** , el cual se presenta en la ilustración siguiente y se describe a continuación.  
  
 En Analysis Services no hay inicios de sesión. Simplemente se crean roles y se asignan a las cuentas de Windows en el panel **Pertenencia** . Todos los usuarios, incluso los administradores, se conectan a Analysis Servicies con una cuenta de Windows.  
  
 ![Crear rol permisos de base de datos de cuadro de diálogo que muestra](../../analysis-services/multidimensional-models/media/ssas-permsdbrole.png "crear rol permisos de base de datos de cuadro de diálogo que muestra")  
  
 Existen tres tipos de permisos especificados en el nivel de la base de datos.  
  
 **Control total (administrador)** : control total es un permiso que lo engloba todo e incluye capacidades extensas en las bases de datos de Analysis Services, como la capacidad para realizar consultas o procesar objetos en la base de datos, así como administrar la seguridad de los roles. Control total es sinónimo de administrador de base de datos. Cuando selecciona **Full Control**, los permisos **Process Database** y **Read Definition** también se seleccionan y no se pueden quitar.  
  
> [!NOTE]  
>  Los administradores de servidor (miembros del rol de administrador de servidor) también disponen de Control total implícito sobre todas las bases de datos del servidor.  
  
 **Procesar base de datos** : este permiso se usa para delegar el procesamiento en el nivel de la base de datos. Como administrador, puede descargar esta tarea si crea un rol que permita que otra persona o servicio invoque las operaciones de procesamiento para cualquier objeto en la base de datos. Si lo prefiere, puede crear roles que permitan realizar el procesamiento en objetos específicos. Vea [Otorgar permisos de procesamiento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md) para obtener más información.  
  
 **Leer definición** : este permiso otorga la capacidad de leer metadatos de objeto, pero no para ver los datos asociados. Por lo general, este permiso se usa en roles que se crearon para el procesamiento dedicado, e incorpora la capacidad de usar herramientas como [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para procesar una base de datos de forma interactiva. Sin **Read Definition**, el permiso **Process Database** solamente resulta efectivo en escenarios con scripts. Si tiene previsto automatizar el procesamiento, quizás a través de SSIS u otro programador, se recomienda crear un rol que tenga **Process Database** sin **Read Definition**. De lo contrario, es conveniente combinar las dos propiedades en el mismo rol para admitir el procesamiento desatendido e interactivo mediante herramientas de SQL Server que visualizan el modelo de datos en una interfaz de usuario.  
  
## <a name="full-control-administrator-permissions"></a>Permisos de Control total (administrador)  
 En [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], un administrador de base de datos es una identidad de usuario de Windows que se asigna a un rol y que incluye permisos de Control total (administrador). Un administrador de base de datos puede realizar cualquier tarea en la base de datos, lo cual incluye:  
  
-   Procesar objetos  
  
-   Leer datos y metadatos para todos los objetos de la base de datos, lo cual incluye cubos, dimensiones, grupos de medida, perspectivas y modelos de minería de datos  
  
-   Crear o modificar roles de base de datos; para ello se agregan usuarios o permisos, lo cual incluye agregar usuarios a roles que disponen también de permisos de Control total  
  
-   Eliminar roles de base de datos o la pertenencia a roles  
  
-   Registre ensamblados (o procedimientos almacenados) para la base de datos.  
  
 Tenga en cuenta que un administrador de base de datos no puede agregar o eliminar bases de datos en el servidor ni otorgar derechos de administrador a otras bases de datos en el mismo servidor. Ese privilegio corresponde exclusivamente al administrador del servidor. Para más información sobre este nivel de permisos, vea [Conceder permisos de administrador de servidor (Analysis Services)](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md) .  
  
 Dado que todos los roles están definidos por el usuario, se recomienda que cree un rol dedicado para este fin (por ejemplo, un rol denominado "dbadmin") y, después, que asigne cuentas de usuario y grupo de Windows según corresponda.  
  
#### <a name="create-roles-in-ssms"></a>Crear roles en SSMS  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], abra la carpeta **Bases de datos** , seleccione una base de datos y haga clic con el botón derecho en **Roles** | **Nuevo rol**.  
  
2.  En el panel **General** , especifique un nombre, como DBAdmin.  
  
3.  Active la casilla **Control total (administrador)** para el cubo. Tenga en cuenta que **Process Database** y **Read Definition** se seleccionan de forma automática. Estos permisos están siempre comprendidos en roles que incluyen **Full Control**.  
  
4.  En el panel **Pertenencia** , especifique las cuentas de usuario y grupo de Windows que se conectan a Analysis Services con este rol.  
  
5.  Haga clic en **Aceptar** para completar la creación del rol.  
  
## <a name="process-database"></a>Process Database  
 Cuando defina un rol que otorgue permisos de base de datos, puede omitir **Control total** y elegir simplemente **Procesar base de datos**. Este permiso, que se establece en el nivel de la base de datos, permite el procesamiento en todos los objetos de la base de datos. Vea [Otorgar permisos de procesamiento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
## <a name="read-definition"></a>Read Definition  
 Al igual que **Procesar base de datos**, si se establecen los permisos de **Leer definición** en el nivel de la base de datos se produce un efecto en cascada sobre los otros objetos de la base de datos. Si quiere establecer permisos de Leer definición a un nivel más granular, debe desactivar Leer definición como propiedad de base de datos en el panel General. Para más información, vea [Otorgar permisos Leer definición en metadatos de objetos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Conceder permisos de administrador de servidor (Analysis Services)](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Otorgar permisos de procesamiento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
  


---
title: "Las extensiones de personalización de Analysis Services | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: personalization extensions [Multidimensional Databases]
ms.assetid: 0f144059-24e0-40c0-bde4-d48c75e46598
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bcc21da9d0f0297bf5db834d3ec66acdb3be397a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="analysis-services-personalization-extensions"></a>Extensiones de personalización de Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] extensiones de personalización constituyen el fundamento de la idea de implementar una arquitectura de complemento. En una arquitectura de este tipo se pueden desarrollar de forma dinámica nuevos objetos y funcionalidad de cubo, y compartirlos fácilmente con otros programadores. Por lo tanto, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] las extensiones de personalización proporcionan la funcionalidad que permite lograr lo siguiente:  
  
-   **Diseño e implementación dinámicos** inmediatamente después de diseñar e implementar [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] extensiones de personalización, los usuarios tienen acceso a los objetos y la funcionalidad al principio de la siguiente sesión de usuario.  
  
-   **Independencia de la interfaz** independientemente de la interfaz que se usa para crear el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] extensiones de personalización, los usuarios pueden utilizar cualquier interfaz para tener acceso a objetos y funcionalidades.  
  
-   **Contexto de la sesión** [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] extensiones de personalización no son objetos permanentes en la infraestructura existente y no se requieren que se vuelva a procesar el cubo. Se exponen y se crean para el usuario en el momento en que este se conecta a la base de datos, y permanecen disponibles durante esa sesión de usuario.  
  
-   **Distribución rápida** recurso compartido [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] extensiones de personalización con otros desarrolladores de software sin tener que entrar en especificaciones detalladas sobre dónde o cómo buscar esta funcionalidad extendida.  
  
 Las extensiones de personalización de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] tienen muchos usos. Por ejemplo, supongamos que su compañía tiene ventas que implican monedas diferentes. Crea un miembro calculado que devuelve las ventas consolidadas en la moneda local de la persona que está teniendo acceso al cubo. Crea este miembro como una extensión de personalización. A continuación, comparte este miembro calculado con un grupo de usuarios. Una vez compartido, los usuarios tienen acceso inmediato al miembro calculado en cuanto se conectan al servidor. Tienen acceso aunque no usen la misma interfaz que la que se usó para crear el miembro calculado.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]las extensiones de personalización son una modificación simple y elegante de la arquitectura de ensamblado administrado existente y se exponen en la [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] <xref:Microsoft.AnalysisServices.AdomdServer> objeto modelo, la sintaxis de expresiones multidimensionales (MDX) y conjuntos de filas de esquema.  
  
## <a name="logical-architecture"></a>Arquitectura lógica  
 La arquitectura de las extensiones de personalización de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] se basa en la arquitectura de ensamblado administrado y en los cuatro elementos básicos siguientes:  
  
 El atributo personalizado [PlugInAttribute]  
 Al iniciar el servicio, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] carga los ensamblados necesarios y determina qué clases tienen el <xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute> atributo personalizado.  
  
> [!NOTE]  
>  [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] define los atributos personalizados como una manera de describir el código e influir en el comportamiento en tiempo de ejecución. Para obtener más información, vea el tema "[Attributes Overview](http://go.microsoft.com/fwlink/?LinkId=82929)," en el [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Guía del desarrollador en MSDN.  
  
 Para todas las clases con el <xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute> atributo personalizado, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] sus constructores predeterminados, se invoca. Invocar todos los constructores en el inicio proporciona una ubicación común para generar nuevos objetos y que es independiente de cualquier actividad de usuario.  
  
 Además de generar una pequeña memoria caché de información sobre la creación y administración de las extensiones de personalización, el constructor de clase se suscribe normalmente a los eventos <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened> y <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing>. Si no se produce la suscripción a estos eventos, es posible que el recolector de elementos no utilizados de Common Language Runtime (CLR) marque de forma inadecuada la clase para la limpieza.  
  
 Contexto de la sesión  
 Para los objetos que se basan en extensiones de personalización, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] crea un entorno de ejecución durante la sesión del cliente y genera dinámicamente la mayor parte de esos objetos en este entorno. Como cualquier otro ensamblado de CLR, este entorno de ejecución también tiene acceso a otras funciones y procedimientos almacenados. Cuando finaliza la sesión de usuario, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] quita los objetos creados de forma dinámica y se cierra el entorno de ejecución.  
  
 Eventos  
 Creación de objetos se desencadena los eventos de sesión **OpenedCubeOpened en cubos** y **ClosingCubeClosing en cubos**.  
  
 La comunicación entre el cliente y el servidor se produce a través de eventos concretos. Estos eventos hacen que el cliente conozca las situaciones que conducen a que se generen los objetos del cliente. El entorno del cliente se crea dinámicamente mediante el uso de dos conjuntos de eventos: eventos de sesión y eventos de cubo.  
  
 Los eventos de sesión se asocian al objeto de servidor. Cuando un cliente inicia sesión en un servidor, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] crea una sesión y desencadena el <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened> eventos. Cuando un cliente finaliza la sesión en el servidor, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] desencadenadores el <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing> eventos.  
  
 Los eventos de cubo se asocian al objeto de conexión. La conexión a un cubo desencadena el evento <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeOpened>. El cierre de la conexión a un cubo, ya sea cerrándolo o cambiando a un cubo diferente, desencadena un evento <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeClosing>.  
  
 Seguimiento y control de errores  
 Toda la actividad puede ser objeto de seguimiento mediante el uso de [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]. Los errores no controlados se notifican al registro de eventos de Windows.  
  
 Toda la creación y administración de objetos es independiente de esta arquitectura y es responsabilidad exclusiva de los programadores de los objetos.  
  
## <a name="infrastructure-foundations"></a>Fundamentos de la infraestructura  
 Las extensiones de personalización de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] se basan en componentes existentes. A continuación se muestra un resumen de las mejoras que proporciona la funcionalidad de las extensiones de personalización.  
  
### <a name="assemblies"></a>Ensamblados  
 El atributo personalizado, <xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute>, se puede agregar a los ensamblados personalizados para identificar las clases de extensiones de personalización de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
### <a name="changes-to-the-adomdserver-object-model"></a>Cambios del modelo de objetos AdomdServer  
 Los objetos siguientes del modelo de objetos <xref:Microsoft.AnalysisServices.AdomdServer> se han mejorado o se han agregado al modelo.  
  
#### <a name="new-adomdconnection-class"></a>Nueva clase AdomdConnection  
 La clase <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection> es nueva y expone varias extensiones de personalización a través de propiedades y eventos.  
  
 **Propiedades**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.SessionID%2A>, un valor de cadena de solo lectura que representa el identificador de sesión de la conexión actual.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.ClientCulture%2A>, una referencia de solo lectura a la referencia cultural del cliente asociada a la sesión actual.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.User%2A>, una referencia de solo lectura a la interfaz de identidad que representa al usuario actual.  
  
 **Eventos**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeOpened>  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeClosing>  
  
#### <a name="new-properties-in-the-context-class"></a>Nuevas propiedades en la clase Context  
 La clase <xref:Microsoft.AnalysisServices.AdomdServer.Context> tiene dos propiedades nuevas:  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Context.Server%2A>, una referencia de solo lectura al nuevo objeto de servidor.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Context.CurrentConnection%2A>, una referencia de solo lectura al nuevo objeto <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection>.  
  
#### <a name="new-server-class"></a>Nueva clase Server  
 La clase <xref:Microsoft.AnalysisServices.AdomdServer.Server> es nueva y expone varias extensiones de personalización a través de propiedades y eventos de clase.  
  
 **Propiedades**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.Name%2A>, un valor de cadena de solo lectura que representa el nombre del servidor.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.Culture%2A>, una referencia de solo lectura a la referencia cultural global asociada al servidor.  
  
 **Eventos**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened>  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing>  
  
#### <a name="adomdcommand-class"></a>Clase AdomdCommand  
 La clase <xref:Microsoft.AnalysisServices.AdomdServer.AdomdCommand> admite ahora los comandos MDX siguientes:  
  
-   [CREATE MEMBER &#40;instrucción MDX&#41;](../../../mdx/mdx-data-definition-create-member.md)  
  
-   [Declaración de miembro UPDATE &#40; MDX &#41;](../../../mdx/mdx-data-definition-update-member.md)  
  
-   [DROP MEMBER, instrucción &#40; MDX &#41;](../../../mdx/mdx-data-definition-drop-member.md)  
  
-   [CREATE SET &#40;Instrucción, MDX&#41;](../../../mdx/mdx-data-definition-create-set.md)  
  
-   [QUITE la instrucción SET &#40; MDX &#41;](../../../mdx/mdx-data-definition-drop-set.md)  
  
-   [CREAR KPI, instrucción &#40; MDX &#41;](../../../mdx/mdx-data-definition-create-kpi.md)  
  
-   [Eliminar KPI, instrucción &#40; MDX &#41;](../../../mdx/mdx-data-definition-drop-kpi.md)  
  
### <a name="mdx-extensions-and-enhancements"></a>Extensiones y mejoras de MDX  
 El comando CREATE MEMBER se mejora con la **título** propiedad, el **display_folder** propiedad y el **associated_measure_group** propiedad.  
  
 El comando UPDATE MEMBER se agrega para no tener que crear de nuevo los miembros cuando se necesita una actualización con la consiguiente pérdida de prioridad en la resolución de cálculos. Las actualizaciones no pueden cambiar el ámbito del miembro calculado, mover el miembro calculado a un elemento primario diferente o definir otro **solveorder**.  
  
 El comando CREATE SET se mejora con la **título** propiedad, el **display_folder** propiedad y el nuevo **estático | DINÁMICA** palabra clave. *Estática* significa que el conjunto se evalúa solo en el momento de creación. *Dinámica* significa que el conjunto se evalúa cada vez que el conjunto se utiliza en una consulta. El valor predeterminado es **estático** si se omite una palabra clave.  
  
 Los comandos CREATE KPI y DROP KPI se agregan a la sintaxis de MDX. Las KPI se pueden crear dinámicamente a partir de cualquier script MDX.  
  
### <a name="schema-rowsets-extensions"></a>Extensiones de conjuntos de filas de esquema  
 En MDSCHEMA_MEMBERS *ámbito* se agrega la columna. Los valores de scope son los siguientes: MDMEMBER_SCOPE_GLOBAL=1, MDMEMBER_SCOPE_SESSION=2.  
  
 En MDSCHEMA_SETS *set_evaluation_context* se agrega la columna. Los valores de set evaluation context son los siguientes: MDSET_RESOLUTION_STATIC = 1, MDSET_RESOLUTION_DYNAMIC = 2.  
  
 En MDSCHEMA_KPIS se agrega la columna scope. Los valores de scope son los siguientes: MDKPI_SCOPE_GLOBAL=1, MDKPI_SCOPE_SESSION=2.  
  
  

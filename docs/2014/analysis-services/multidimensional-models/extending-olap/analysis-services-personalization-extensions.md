---
title: Extensiones de personalización de Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- personalization extensions [Multidimensional Databases]
ms.assetid: 0f144059-24e0-40c0-bde4-d48c75e46598
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0cd36cb2882659bff902d9830af0c5acefd98444
ms.sourcegitcommit: 04ba0ed3d860db038078609d6e348b0650739f55
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468980"
---
# <a name="analysis-services-personalization-extensions"></a>Extensiones de personalización de Analysis Services
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]las [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] extensiones de personalización son la base de la idea de implementar una arquitectura de complemento. En una arquitectura de este tipo se pueden desarrollar de forma dinámica nuevos objetos y funcionalidad de cubo, y compartirlos fácilmente con otros programadores. Como tal, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] las extensiones de personalización proporcionan la funcionalidad que permite lograr lo siguiente:  
  
-   **Diseño e implementación dinámicos** Inmediatamente después de diseñar e implementar [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] las extensiones de personalización, los usuarios tienen acceso a los objetos y la funcionalidad al inicio de la siguiente sesión de usuario.  
  
-   **Independencia** de la interfaz Independientemente de la interfaz que use para crear las [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] extensiones de personalización, los usuarios pueden utilizar cualquier interfaz para tener acceso a los objetos y a la funcionalidad.  
  
-   **Contexto** [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] de sesión las extensiones de personalización no son objetos permanentes en la infraestructura existente y no requieren que se vuelva a procesar el cubo. Se exponen y se crean para el usuario en el momento en que este se conecta a la base de datos, y permanecen disponibles durante esa sesión de usuario.  
  
-   **Distribución rápida** Comparta [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] las extensiones de personalización con otros desarrolladores de software sin tener que entrar en especificaciones detalladas sobre dónde o cómo encontrar esta funcionalidad extendida.  
  
 Las extensiones de personalización de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] tienen muchos usos. Por ejemplo, supongamos que su compañía tiene ventas que implican monedas diferentes. Crea un miembro calculado que devuelve las ventas consolidadas en la moneda local de la persona que está teniendo acceso al cubo. Crea este miembro como una extensión de personalización. A continuación, comparte este miembro calculado con un grupo de usuarios. Una vez compartido, esos usuarios tienen acceso inmediato al miembro calculado en cuanto se conectan al servidor. Tienen acceso aunque no usen la misma interfaz que la que se usó para crear el miembro calculado.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]las extensiones de personalización son una modificación simple y elegante de la arquitectura de ensamblado administrado existente y se exponen en el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] modelo de objetos [Microsoft. AnalysisServices. AdomdServer](/previous-versions/sql/sql-server-2014/ms131779(v=sql.120)) , la sintaxis de expresiones multidimensionales (MDX) y los conjuntos de filas de esquema.  
  
## <a name="logical-architecture"></a>Arquitectura lógica  
 La arquitectura de las extensiones de personalización de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] se basa en la arquitectura de ensamblado administrado y en los cuatro elementos básicos siguientes:  
  
 El atributo personalizado [PlugInAttribute]  
 Al iniciar el servicio, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] carga los ensamblados necesarios y determina qué clases tienen el atributo personalizado [Microsoft. AnalysisServices. AdomdServer. PlugInAttribute](/previous-versions/sql/sql-server-2014/bb678014(v=sql.120)) .  
  
> [!NOTE]  
>  [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] define los atributos personalizados como una manera de describir el código e influir en el comportamiento en tiempo de ejecución. Para obtener más información, vea el tema "[información general sobre los atributos](https://go.microsoft.com/fwlink/?LinkId=82929)" en la [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Guía del desarrollador de MSDN.  
  
 Para todas las clases con el atributo personalizado [Microsoft. AnalysisServices. AdomdServer. PlugInAttribute](/previous-versions/sql/sql-server-2014/bb678014(v=sql.120)) , [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] invoca sus constructores predeterminados. La llamada a todos los constructores en el inicio proporciona una ubicación común desde la que se pueden generar nuevos objetos y que es independiente de cualquier actividad del usuario.  
  
 Además de crear una pequeña memoria caché de información sobre la creación y administración de extensiones de personalización, el constructor de clase se suscribe normalmente a los eventos [Microsoft. AnalysisServices. AdomdServer. Server. SessionOpened](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120)) y [Microsoft. AnalysisServices. AdomdServer. Server. SessionClosing](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120)) . Si no se produce la suscripción a estos eventos, es posible que el recolector de elementos no utilizados de Common Language Runtime (CLR) marque de forma inadecuada la clase para la limpieza.  
  
 Contexto de la sesión  
 Para los objetos que se basan en extensiones de personalización, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] crea un entorno de ejecución durante la sesión del cliente y genera dinámicamente la mayor parte de esos objetos en este entorno. Como cualquier otro ensamblado de CLR, este entorno de ejecución también tiene acceso a otras funciones y procedimientos almacenados. Cuando finaliza la sesión de usuario, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] quita los objetos creados dinámicamente y cierra el entorno de ejecución.  
  
 Eventos  
 Los eventos de sesión `On-Cube-OpenedCubeOpened` y `On-Cube-ClosingCubeClosing` desencadenan la creación de objetos.  
  
 La comunicación entre el cliente y el servidor se produce a través de eventos concretos. Estos eventos hacen que el cliente conozca las situaciones que conducen a que se generen los objetos del cliente. El entorno del cliente se crea dinámicamente mediante el uso de dos conjuntos de eventos: eventos de sesión y eventos de cubo.  
  
 Los eventos de sesión se asocian al objeto de servidor. Cuando un cliente inicia sesión en un servidor, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] crea una sesión y desencadena el evento [Microsoft. AnalysisServices. AdomdServer. Server. SessionOpened](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120)) . Cuando un cliente finaliza la sesión en el servidor, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] desencadena el evento [Microsoft. AnalysisServices. AdomdServer. Server. SessionClosing](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120)) .  
  
 Los eventos de cubo se asocian al objeto de conexión. Al conectarse a un cubo, se desencadena el evento [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. CubeOpened](/previous-versions/sql/sql-server-2014/bb630581(v=sql.120)) . Al cerrar la conexión a un cubo, al cerrar el cubo o cambiar a otro cubo, se desencadena un evento [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. CubeClosing](/previous-versions/sql/sql-server-2014/bb630371(v=sql.120)) .  
  
 Seguimiento y control de errores  
 Toda la actividad puede ser objeto de seguimiento mediante el uso de [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]. Los errores no controlados se notifican al registro de eventos de Windows.  
  
 Toda la creación y administración de objetos es independiente de esta arquitectura y es responsabilidad exclusiva de los programadores de los objetos.  
  
## <a name="infrastructure-foundations"></a>Fundamentos de la infraestructura  
 Las extensiones de personalización de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] se basan en componentes existentes. A continuación se muestra un resumen de las mejoras que proporciona la funcionalidad de las extensiones de personalización.  
  
### <a name="assemblies"></a>Ensamblados  
 El atributo personalizado, [Microsoft. AnalysisServices. AdomdServer. PlugInAttribute](/previous-versions/sql/sql-server-2014/bb678014(v=sql.120)), se puede Agregar a los ensamblados personalizados para identificar [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] las clases de extensiones de personalización.  
  
### <a name="changes-to-the-adomdserver-object-model"></a>Cambios del modelo de objetos AdomdServer  
 Los objetos siguientes en el modelo de objetos [Microsoft. AnalysisServices. AdomdServer](/previous-versions/sql/sql-server-2014/ms131779(v=sql.120)) se han mejorado o agregado al modelo.  
  
#### <a name="new-adomdconnection-class"></a>Nueva clase AdomdConnection  
 La clase [Microsoft. AnalysisServices. AdomdServer. AdomdConnection](/previous-versions/sql/sql-server-2014/bb678193(v=sql.120)) es nueva y expone varias extensiones de personalización a través de propiedades y eventos.  
  
 **Propiedades**  
  
-   [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. SessionID *](/previous-versions/sql/sql-server-2014/bb678099(v=sql.120)), un valor de cadena de solo lectura que representa el ID. de sesión de la conexión actual.  
  
-   [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. ClientCulture *](/previous-versions/sql/sql-server-2014/bb677433(v=sql.120)), una referencia de solo lectura a la referencia cultural del cliente asociada a la sesión actual.  
  
-   [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. User *](/previous-versions/sql/sql-server-2014/bb630315(v=sql.120)), una referencia de solo lectura a la interfaz de identidad que representa al usuario actual.  
  
 **Eventos**  
  
-   [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. CubeOpened](/previous-versions/sql/sql-server-2014/bb630581(v=sql.120))  
  
-   [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. CubeClosing](/previous-versions/sql/sql-server-2014/bb630371(v=sql.120))  
  
#### <a name="new-properties-in-the-context-class"></a>Nuevas propiedades en la clase Context  
 La clase [Microsoft. AnalysisServices. AdomdServer. Context](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120)) tiene dos nuevas propiedades:  
  
-   [Microsoft. AnalysisServices. AdomdServer. Context. Server *](/previous-versions/sql/sql-server-2014/bb678098(v=sql.120)), una referencia de solo lectura al nuevo objeto de servidor.  
  
-   [Microsoft. AnalysisServices. AdomdServer. Context. CurrentConnection *](/previous-versions/sql/sql-server-2014/bb630975(v=sql.120)), una referencia de solo lectura al nuevo objeto [Microsoft. AnalysisServices. AdomdServer. AdomdConnection](/previous-versions/sql/sql-server-2014/bb678193(v=sql.120)) .  
  
#### <a name="new-server-class"></a>Nueva clase Server  
 La clase [Microsoft. AnalysisServices. AdomdServer. Server](/previous-versions/sql/sql-server-2014/bb677955(v=sql.120)) es nueva y expone varias extensiones de personalización a través de propiedades y eventos de clase.  
  
 **Propiedades**  
  
-   [Microsoft.AnalysisServices.AdomdServer.Server.Name *](/previous-versions/sql/sql-server-2014/bb677694(v=sql.120)), un valor de cadena de solo lectura que representa el nombre del servidor.  
  
-   [Microsoft. AnalysisServices. AdomdServer. Server. Culture *](/previous-versions/sql/sql-server-2014/bb677437(v=sql.120)), una referencia de solo lectura a la referencia cultural global asociada al servidor.  
  
 **Eventos**  
  
-   [Microsoft. AnalysisServices. AdomdServer. Server. SessionOpened](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120))  
  
-   [Microsoft. AnalysisServices. AdomdServer. Server. SessionClosing](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120))  
  
#### <a name="adomdcommand-class"></a>Clase AdomdCommand  
 La clase [Microsoft. AnalysisServices. AdomdServer. AdomdCommand](/previous-versions/sql/sql-server-2014/ms143286(v=sql.120)) ahora es compatible con los siguientes comandos MDX:  
  
-   [CREATE MEMBER &#40;instrucción MDX&#41;](/sql/mdx/mdx-data-definition-create-member)  
  
-   [Instrucción UPDATE MEMBER &#40;MDX&#41;](/sql/mdx/mdx-data-definition-update-member)  
  
-   [Instrucción DROP MEMBER &#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-member)  
  
-   [CREATE SET &#40;Instrucción, MDX&#41;](/sql/mdx/mdx-data-definition-create-set)  
  
-   [DROP SET, instrucción &#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-set)  
  
-   [CREATE KPI, instrucción &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-kpi)  
  
-   [DROP KPI, instrucción &#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-kpi)  
  
### <a name="mdx-extensions-and-enhancements"></a>Extensiones y mejoras de MDX  
 El comando CREATE MEMBER se mejora con las propiedades `caption`, `display_folder` y `associated_measure_group`.  
  
 El comando UPDATE MEMBER se agrega para no tener que crear de nuevo los miembros cuando se necesita una actualización con la consiguiente pérdida de prioridad en la resolución de cálculos. Las actualizaciones no pueden cambiar el ámbito del miembro calculado, mover el miembro calculado a un elemento primario diferente o definir un `solveorder` distinto.  
  
 El comando CREATE SET se mejora con las propiedades `caption` y `display_folder`, y la nueva palabra clave `STATIC | DYNAMIC`. *Static* significa que el conjunto solo se evalúa en el momento de la creación. *Dynamic* significa que el conjunto se evalúa cada vez que se usa el conjunto en una consulta. El valor predeterminado es `STATIC` si se omite una palabra clave.  
  
 Los comandos CREATE KPI y DROP KPI se agregan a la sintaxis de MDX. Las KPI se pueden crear dinámicamente a partir de cualquier script MDX.  
  
### <a name="schema-rowsets-extensions"></a>Extensiones de conjuntos de filas de esquema  
 En MDSCHEMA_MEMBERS se agrega la columna *ámbito* . Los valores de scope son los siguientes: MDMEMBER_SCOPE_GLOBAL=1, MDMEMBER_SCOPE_SESSION=2.  
  
 En MDSCHEMA_SETS se agrega *set_evaluation_context* columna. Los valores de set evaluation context son los siguientes: MDSET_RESOLUTION_STATIC = 1, MDSET_RESOLUTION_DYNAMIC = 2.  
  
 En MDSCHEMA_KPIS se agrega la columna scope. Los valores de scope son los siguientes: MDKPI_SCOPE_GLOBAL=1, MDKPI_SCOPE_SESSION=2.  
  
  

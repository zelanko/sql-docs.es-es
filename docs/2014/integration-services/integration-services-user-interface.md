---
title: Interfaz de usuario de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services, SSIS Designer
- tools [Integration Services], SSIS Designer
- SSIS Designer
- SSIS, SSIS Designer
- Integration Services, SSIS Designer
ms.assetid: d2c48cff-46f4-4c70-b1f3-c88f9b8757f3
caps.latest.revision: 52
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 72d10ae01b290425d5f00054d84311323c3332a9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37290991"
---
# <a name="integration-services-user-interface"></a>Interfaz de usuario de Integration Services
  Además de las superficies de diseño de las pestañas del Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] , la interfaz de usuario proporciona acceso a las siguientes ventanas y cuadros de diálogo para agregar características a paquetes y configurar las propiedades de los objetos de paquete:  
  
-   Los cuadros de diálogo y ventanas que usa para agregar funcionalidad tal como registros y configuraciones a los paquetes.  
  
-   Los editores personalizados para configurar las propiedades de los objetos de paquete. Prácticamente todos los tipos de componentes de flujo de datos, contenedores y tareas tienen su propio editor personalizado.  
  
-   El cuadro de diálogo **Editor avanzado** , un editor genérico que proporciona opciones más detalladas de configuración para varios componentes de flujo de datos.  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] también proporciona ventanas y cuadros de diálogo para configurar el entorno y trabajar con paquetes.  
  
## <a name="dialog-boxes-and-windows"></a>Cuadros de diálogo y ventanas  
 Después de abrir un paquete o crear un nuevo paquete en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , se pueden usar los siguientes cuadros de diálogo y ventanas.  
  
 La tabla enumera los cuadros de diálogo disponibles en el menú **SSIS** y las superficies de diseño del Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
|Cuadro de diálogo|Finalidad|Acceso|  
|----------------|-------------|------------|  
|**Introducción**|Tener acceso a ejemplos, tutoriales y vídeos.|En la superficie de diseño de la pestaña **Flujo de control** o de la pestaña **Flujo de datos** , haga clic con el botón derecho y elija **Introducción**.<br /><br /> Para mostrar automáticamente la ventana **Introducción** cada vez que cree un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , seleccione **Mostrar siempre en los proyectos nuevos** en la parte inferior de la ventana.|  
|**Configurar registros SSIS**|Configurar el registro de un paquete y sus tareas agregando registros y configurando detalles de registro.|En el menú **SSIS** , haga clic en **Registro**.<br /><br /> - O bien -<br /><br /> Haga clic con el botón derecho en cualquier punto de la superficie de diseño de la pestaña **Flujo de control** y, luego, haga clic en **Registro**.|  
|**Organizador de configuraciones de paquetes**|Agregar y editar configuraciones de paquetes Desde este cuadro de diálogo se ejecuta el Asistente para la configuración de paquetes.|En el menú **SSIS** , haga clic en **Configuraciones de paquetes**.<br /><br /> -o bien-<br /><br /> Haga clic con el botón derecho en cualquier punto de la superficie de diseño de la pestaña **Flujo de control** y, luego, haga clic en **Configuraciones de paquetes**.|  
|**Firma digital**|Firmar un paquete o quitar la firma del paquete.|En el menú **SSIS** , haga clic en **Firma digital**.<br /><br /> -o bien-<br /><br /> Haga clic con el botón derecho en cualquier punto de la superficie de diseño de la pestaña **Flujo de control** y, luego, haga clic en **Firma digital**.|  
|**Establecer puntos de interrupción**|Habilitar puntos de interrupción en tareas y establecer las propiedades de los puntos de interrupción.|En la superficie de diseño de la pestaña **Flujo de control** , haga clic con el botón derecho en una tarea o contenedor y, luego, haga clic en **Editar puntos de interrupción**. Para establecer un punto de interrupción en el paquete, haga clic con el botón derecho en cualquier punto de la superficie de diseño de la pestaña **Flujo de control** y, luego, haga clic en **Editar puntos de interrupción**.|  
  
 La ventana de **Introducción** proporciona vínculos a ejemplos, tutoriales y vídeos. Para agregar vínculos al contenido adicional, modifique el archivo SamplesSites.xml que se incluye con la versión actual de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Se recomienda que no modifique el valor del elemento \<GettingStartedSamples> que especifica la dirección URL de la fuente RSS. El archivo se encuentra en la carpeta *unidad>\<*:\Archivos de programa\Microsoft SQL Server\110\DTS\Binn. En un equipo de 64 bits, el archivo se encuentra en la carpeta *\<unidad>*:\Archivos de programa(x86)\Microsoft SQL Server\110\DTS\Binn.  
  
 Si el archivo SamplesSites.xml se daña, reemplace el XML del archivo por el XML predeterminado siguiente.  
  
 `<?xml version="1.0" ?>`  
  
 `- <SamplesSites>`  
  
 `<GettingStartedSamples>http://go.microsoft.com/fwlink/?LinkID=203147</GettingStartedSamples>`  
  
 `- <ToolboxSamples>`  
  
 `<Site>http://go.microsoft.com/fwlink/?LinkID=203286&query=SSIS%20{0}</Site>`  
  
 `</ToolboxSamples>`  
  
 `</SamplesSites>`  
  
 En esta tabla se enumeran las ventanas disponibles desde los menús **SSIS** y **Ver** , y las superficies de diseño del Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
|Ventana|Finalidad|Acceso|  
|------------|-------------|------------|  
|**Variables**|Agregar y administrar variables personalizadas.|En el menú **SSIS** , haga clic en **Variables**.<br /><br /> -o bien-<br /><br /> Haga clic con el botón derecho en cualquier punto de la superficie de diseño de las pestañas **Flujo de control** y **Flujo de datos** y, luego, haga clic en **Variables**.<br /><br /> -o bien-<br /><br /> En el menú **Ver** , seleccione **Otras ventanas**y haga clic en **Variables**.|  
|**Registrar eventos**|Ver entradas del registro en tiempo de ejecución.|En el menú **SSIS** , haga clic en **Registrar eventos**.<br /><br /> -o bien-<br /><br /> Haga clic con el botón derecho en cualquier punto de la superficie de diseño de las pestañas **Flujo de control** y **Flujo de datos** y, luego, haga clic en **Registrar eventos**.<br /><br /> -o bien-<br /><br /> En el menú **Ver** , seleccione **Otras ventanas**y haga clic en **Registrar eventos**.|  
  
## <a name="custom-editors"></a>Editores personalizados  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proporciona un cuadro de diálogo personalizado para la mayoría de los contenedores, tareas, orígenes, transformaciones y destinos.  
  
 La siguiente tabla describe cómo obtener acceso a los cuadros de diálogo personalizados.  
  
|Tipo de editor|Acceso|  
|-----------------|------------|  
|Contenedor. Para más información, vea [Contenedores de Integration Services](control-flow/integration-services-containers.md).|En la superficie de diseño de la pestaña **Flujo de control** , haga doble clic en el contenedor.|  
|Tarea. Para más información, consulte [Integration Services Tasks](control-flow/integration-services-tasks.md).|En la superficie de diseño de la pestaña **Flujo de control** , haga doble clic en la tarea.|  
|Origen.|En la superficie de diseño de la pestaña **Flujo de control** , haga doble clic en el origen.|  
|Transformación. Para más información, consulte [Integration Services Transformations](data-flow/transformations/integration-services-transformations.md).|En la superficie de diseño de la pestaña **Flujo de control** , haga doble clic en la transformación.|  
|Destino.|En la superficie de diseño de la pestaña **Flujo de control** , haga doble clic en el destino.|  
  
## <a name="advanced-editor"></a>Editor avanzado  
 El cuadro de diálogo **Editor avanzado** es una interfaz de usuario para configurar componentes de flujo de datos. Refleja las propiedades del componente mediante un diseño genérico. El cuadro de diálogo **Editor avanzado** no está disponible para las transformaciones de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que tienen varias entradas.  
  
 Para abrir este editor, haga clic en **Mostrar editor avanzado** en la ventana **Propiedades** o haga clic con el botón derecho en un componente de flujo de datos y, luego, haga clic en **Mostrar editor avanzado**.  
  
 Si crea un origen, transformación o destino personalizado pero no desea escribir una interfaz de usuario personalizada, puede usar el **Editor avanzado** en su lugar.  
  
## <a name="sql-server-data-tools-features"></a>Características de las herramientas de datos de SQL Server  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] proporciona ventanas, cuadros de diálogo y opciones de menú para trabajar con paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 Lo siguiente es un resumen de las ventanas y menús disponibles:  
  
-   La ventana **Explorador de soluciones** enumera proyectos, incluido el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en el que se desarrollan paquetes [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , y archivos de proyecto.  
  
     Para ordenar los paquetes que contiene un proyecto según el nombre, haga clic con el botón derecho en el nodo **Paquetes SSIS** y, después, haga clic en **Ordenar por nombre**.  
  
-   La ventana **Cuadro de herramientas** enumera los elementos de flujo de control y flujo de datos para generar flujos de control y flujos de datos.  
  
-   La ventana **Propiedades** enumera las propiedades de los objetos.  
  
-   El menú **Formato** proporciona opciones de ajuste de tamaño y alineación de controles en un paquete.  
  
-   El menú **Edición** proporciona funciones de copiado y pegado para copiar objetos en las superficies de diseño.  
  
-   El menú **Ver** proporciona opciones para modificar la representación gráfica de objetos en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)]   
  
 Para obtener más información sobre otras ventanas y menús, vea la documentación sobre Visual Studio.  
  
## <a name="related-tasks"></a>Related Tasks  
 Para más información sobre cómo crear paquetes en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], vea [Crear paquetes en SQL Server Data Tools](create-packages-in-sql-server-data-tools.md).  
  
## <a name="see-also"></a>Vea también  
 [Diseñador SSIS](ssis-designer.md)  
  
  

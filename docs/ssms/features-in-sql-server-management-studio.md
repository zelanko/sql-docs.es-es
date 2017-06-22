---
title: "Características de SQL Server Management Studio | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], about SQL Server Management Studio
- scripts [SQL Server], SQL Server Management Studio
ms.assetid: e75504b9-7968-4e3b-8411-fd79fe09021e
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 82a8f1c09d51ad35b9d61e68b6878dc90b7d617c
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="features-in-sql-server-management-studio"></a>Características de SQL Server Management Studio
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] incluye las siguientes características generales:  
  
-   Compatibilidad con la mayoría de las tareas administrativas de [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)].  
  
-   Un entorno único integrado para la administración del [!INCLUDE[ssDEnoversion](../includes/ssdenoversion_md.md)] y la creación.  
  
-   Cuadros de diálogo para administrar objetos de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion_md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)]y [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion_md.md)], lo que permite ejecutar las acciones inmediatamente, enviarlas a un editor de código o escribirlas en script para ejecutarlas posteriormente.  
  
-   Cuadros de diálogo no modales y de tamaño variable que permiten obtener acceso a varias herramientas mientras un cuadro de diálogo está abierto.  
  
-   Un cuadro de diálogo común de programación que permite realizar acciones de los cuadros de diálogo de administración en otro momento.  
  
-   Exportación e importación del registro de servidor de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] desde un entorno de [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] a otro.  
  
-   Guardado o impresión de archivos de plan de presentación XML o de interbloqueo generados por SQL Server Profiler, revisión posterior o envío a los administradores para su análisis.  
  
-   Un nuevo cuadro de mensaje de error e informativo que presenta mucha más información, permite enviar a [!INCLUDE[msCoName](../includes/msconame_md.md)] un comentario sobre los mensajes, copiar mensajes en el Portapapeles y enviar fácilmente los mensajes por correo electrónico al equipo de soporte.  
  
-   Un explorador web integrado para una rápida exploración de MSDN o la Ayuda en pantalla.  
  
-   Integración de la Ayuda de comunidades en línea.  
  
-   Un tutorial sobre [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] para ayudarle a aprovechar las ventajas de las numerosas características nuevas y a que sea más productivo de forma inmediata.  
  
-   Un nuevo monitor de actividad con filtro y actualización automática.  
  
-   Interfaces de Correo electrónico de base de datos integradas.  
  
## <a name="new-scripting-capabilities"></a>Nuevas funciones de scripting  
El componente Editor de código de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] contiene editores de script integrados para crear [!INCLUDE[tsql](../includes/tsql_md.md)], MDX, DMX y XML/A. Ofrece las características siguientes:  
  
-   Ayuda dinámica para el acceso inmediato a la información relevante mientras se trabaja.  
  
-   Un amplio conjunto de plantillas y la posibilidad de crear plantillas personalizadas.  
  
-   Compatibilidad con la escritura y modificación de consultas o scripts sin necesidad de conexión a un servidor.  
  
-   Compatibilidad con scripting para consultas y scripts SQLCMD.  
  
-   Una nueva interfaz para ver resultados XML.  
  
-   Control de código fuente integrado para proyectos de script y soluciones compatible con el almacenamiento y la conservación de copias de scripts a medida que evolucionan.  
  
-   [!INCLUDE[msCoName](../includes/msconame_md.md)] Compatibilidad de IntelliSense con instrucciones MDX.  
  
## <a name="object-explorer-features"></a>Características del Explorador de objetos  
El Explorador de objetos de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] es una herramienta integrada para ver y administrar objetos en todo tipo de servidores. Ofrece las características siguientes:  
  
-   Filtrado por todo o parte de un nombre, esquema o fecha.  
  
-   Llenado asincrónico de objetos, con la posibilidad de filtrar objetos según sus metadatos.  
  
-   Acceso al Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] en los servidores de replicación para administración.  
  
Para obtener más información, vea [Explorador de objetos](../ssms/object/object-explorer.md).  
  
## <a name="extensibility"></a>Extensibilidad  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] se basa en el shell aislado de Visual Studio, que admite la extensibilidad de forma inherente (complementos). Es posible aprovechar los servicios de extensibilidad de Visual Studio para descubrir las capacidades personalizadas en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]; no obstante, no se admite la extensibilidad.  
  
Hay algunos usuarios y terceros que han desarrollado extensiones para [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]. Aunque no se desaconseja, tenga en cuenta que no se admite dicha extensibilidad, por lo que puede haber problemas con la compatibilidad con versiones anteriores o posteriores. Microsoft no publica documentación para ampliar [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]. Sin embargo, hay blogs de la comunidad y código de ejemplo que podría aprovechar.  
  
Microsoft no admite las instalaciones de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] con las extensiones de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] presentes, por lo que si ha instalado extensiones de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] , puede quitarlas antes de llamar al servicio de soporte al cliente de Microsoft acerca de un problema de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] .  
  
## <a name="see-also"></a>Vea también  
[Usar SQL Server Management Studio](../ssms/use-sql-server-management-studio.md)  
  


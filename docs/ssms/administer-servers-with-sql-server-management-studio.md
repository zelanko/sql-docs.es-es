---
title: Administrar servidores con SQL Server Management Studio | Microsoft Docs
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
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], administering
ms.assetid: 938bb035-e07a-4082-9f93-229d9feb6b06
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d73b15b799fe8c52124331cfc346d3759fc860a6
ms.contentlocale: es-es
ms.lasthandoff: 08/18/2017

---
# <a name="administer-servers-with-sql-server-management-studio"></a>Administrar servidores con SQL Server Management Studio
[!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] es un eficaz cliente integrado diseñado para satisfacer los requisitos de administración de servidores del administrador de Azure SQL Database y [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] . En [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)], las tareas administrativas se realizan mediante el Explorador de objetos, que permite conectarse a cualquier servidor de la familia de [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] y examinar de forma gráfica su contenido. Un servidor puede ser una instancia de [!INCLUDE[ssDE](../includes/ssde_md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion_md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion_md.md)] o Azure SQL Database.  
  
Entre las herramientas que componen [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] se incluyen Servidores registrados, el Explorador de objetos, el Explorador de soluciones, el Explorador de plantillas, la página Detalles del Explorador de objetos y la ventana de documento. Para mostrar una herramienta, haga clic en su nombre en el menú **Ver** . Para mostrar el Editor de consultas, haga clic en el botón **Nueva consulta** de la barra de herramientas.  
  
> [!IMPORTANT]  
> El tráfico de red entre [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] y [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] no está cifrado de forma predeterminada. No trabaje con datos confidenciales (incluidas contraseñas) en [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] a menos que haya establecido una conexión cifrada. Para más información, consulte [Habilitar conexiones cifradas en el motor de base de datos (Administrador de configuración de SQL Server)](http://msdn.microsoft.com/en-us/e1e55519-97ec-4404-81ef-881da3b42006).  
  
Use [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] para:  
  
-   Registrar servidores.  
  
-   Conectarse a una instancia de [!INCLUDE[ssDE](../includes/ssde_md.md)], [!INCLUDE[ssAS](../includes/ssas_md.md)], [!INCLUDE[ssRS](../includes/ssrs_md.md)],  [!INCLUDE[ssIS](../includes/ssis_md.md)] or Azure SQL Database.  
  
-   Configurar las propiedades del servidor.  
  
-   Administrar la base de datos y objetos de [!INCLUDE[ssAS](../includes/ssas_md.md)] , tales como cubos, dimensiones y ensamblados.  
  
-   Crear objetos, tales como bases de datos, tablas, cubos, usuarios de base de datos e inicios de sesión.  
  
-   Administrar archivos y grupos de archivos.  
  
-   Adjuntar o separar bases de datos.  
  
-   Iniciar herramientas de scripting.  
  
-   Administrar la seguridad.  
  
-   Ver registros del sistema.  
  
-   Supervisar la actividad actual.  
  
-   Configurar la replicación.  
  
-   Administrar índices de texto completo.  
  
Para iniciar y detener [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] o el Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] , utilice el Administrador de configuración de [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] .  
  
## <a name="see-also"></a>Vea también  
[Usar SQL Server Management Studio](../ssms/use-sql-server-management-studio.md)  
[Ver las propiedades de un servidor (SQL Server Management Studio)](http://msdn.microsoft.com/en-us/55f3ac04-5626-4ad2-96bd-a1f1b079659d)  
  


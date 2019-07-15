---
title: Administrar servidores con SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], administering
ms.assetid: 938bb035-e07a-4082-9f93-229d9feb6b06
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 16873fad4465056801d0e65d64e96ce2bc818798
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2019
ms.locfileid: "67689072"
---
# <a name="administer-servers-with-sql-server-management-studio"></a>Administrar servidores con SQL Server Management Studio
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] es un eficaz cliente integrado diseñado para satisfacer los requisitos de administración de servidores del administrador de Azure SQL Database y [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . En [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], las tareas administrativas se realizan mediante el Explorador de objetos, que permite conectarse a cualquier servidor de la familia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y examinar de forma gráfica su contenido. Un servidor puede ser una instancia de [!INCLUDE[ssDE](../includes/ssde_md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] o Azure SQL Database.  
  
Entre las herramientas que componen [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] se incluyen Servidores registrados, el Explorador de objetos, el Explorador de soluciones, el Explorador de plantillas, la página Detalles del Explorador de objetos y la ventana de documento. Para mostrar una herramienta, haga clic en su nombre en el menú **Ver** . Para mostrar el Editor de consultas, haga clic en el botón **Nueva consulta** de la barra de herramientas.  
  
> [!IMPORTANT]  
> El tráfico de red entre [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] y [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no está cifrado de forma predeterminada. No trabaje con datos confidenciales (incluidas contraseñas) en [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] a menos que haya establecido una conexión cifrada. Para más información, vea: [Cómo: Habilitar conexiones cifradas en el motor de base de datos (Administrador de configuración de SQL Server)](https://msdn.microsoft.com/e1e55519-97ec-4404-81ef-881da3b42006).  
  
Use [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para:  
  
-   Registrar servidores.  
  
-   Conectarse a una instancia de [!INCLUDE[ssDE](../includes/ssde_md.md)], SSAS, [!INCLUDE[ssRS](../includes/ssrs.md)], [!INCLUDE[ssIS](../includes/ssis_md.md)] o Azure SQL Database.  
  
-   Configurar las propiedades del servidor.  
  
-   Administrar la base de datos y objetos de SSAS, como cubos, dimensiones y ensamblados.  
  
-   Crear objetos, tales como bases de datos, tablas, cubos, usuarios de base de datos e inicios de sesión.  
  
-   Administrar archivos y grupos de archivos.  
  
-   Adjuntar o separar bases de datos.  
  
-   Iniciar herramientas de scripting.  
  
-   Administrar la seguridad.  
  
-   Ver registros del sistema.  
  
-   Supervisar la actividad actual.  
  
-   Configurar la replicación.  
  
-   Administrar índices de texto completo.  
  
Para iniciar y detener [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o el Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , utilice el Administrador de configuración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte también  
[Usar SQL Server Management Studio](../ssms/use-sql-server-management-studio.md)  
[Cómo: Ver las propiedades de un servidor (SQL Server Management Studio)](https://msdn.microsoft.com/55f3ac04-5626-4ad2-96bd-a1f1b079659d)  
  

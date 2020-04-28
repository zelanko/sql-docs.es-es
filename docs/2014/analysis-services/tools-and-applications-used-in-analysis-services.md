---
title: Herramientas y aplicaciones usadas en Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0ddb3b7a-7464-4d04-8659-11cb2e4cf3c3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4a48b400196a77a9c59219bc28cdff496229ae7e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175564"
---
# <a name="tools-and-applications-used-in-analysis-services"></a>Herramientas y aplicaciones utilizadas en Analysis Services
  Encuentre las herramientas y las aplicaciones que necesitará para crear los modelos de Analysis Services y para administrar las bases de datos asociadas en una instancia de Analysis Services.

## <a name="analysis-services-model-designers"></a>Diseñadores de modelo de Analysis Services
 Los modelos tabulares y multidimensionales se crean a partir de plantillas de proyectos en una solución construida dentro del shell de Visual Studio. La plantilla del proyecto proporciona los diseñadores la creación de modelos, cubos, dimensiones y roles y comprenden una solución de Analysis Services.

### <a name="download-sql-server-data-tools-for-business-intelligence-ssdt-bi"></a>Descargue SQL Server Data Tools para Business Intelligence (SSDT-BI)
 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] para Business Intelligence (SSDT-BI), conocido anteriormente como Business Intelligence Development Studio (BIDS), se emplea para crear modelos de Analysis Services, informes de Reporting Services y paquetes de Integration Services. Puede descargar SSDT-BI desde las ubicaciones siguientes:

-   [Descargar SSDT-BI para Visual Studio 2013](https://go.microsoft.com/fwlink/p/?LinkId=396526)

-   [Descargar SSDT-BI para Visual Studio 2012](https://go.microsoft.com/fwlink/p/?LinkID=273673)

 Si tiene instalada en el equipo una versión anterior de SSDT-BI o BIDS, la versión más reciente se instala en paralelo con la versión anterior. Es frecuente ejecutar versiones más recientes y versiones anteriores de las herramientas de diseño en una misma estación de trabajo para poder modificar soluciones y proyectos vinculados a determinadas versiones del servidor.

> [!NOTE]
>  Hay varios sitios de descarga para las versiones de Visual Studio 2012 y Visual Studio 2013 de SSDT. La mayoría no incluyen las plantillas de proyecto BI. En los vínculos anteriores obtendrá la versión correcta. Sabrá que tiene la versión correcta de SSDT-BI si ve la carpeta de plantillas de proyecto de Business Intelligence. Esta carpeta contiene las plantillas de proyecto para Analysis Services, Reporting Services e Integration Services. Según cómo haya instalado SSDT-BI, es posible que vea también una plantilla de proyecto adicional para bases de datos de SQL Server.

 ![Nuevas plantillas de proyecto de SSDT](media/ssdt-biprojects.png "Nuevas plantillas de proyecto de SSDT")

## <a name="administrative-tools"></a>Herramientas administrativas

### <a name="sql-server-management-studio"></a>SQL Server Management Studio
 Management Studio es la herramienta de administración principal para todas las características de SQL Server, incluida Analysis Services. SQL Server Management Studio es un componente opcional. Si no lo ve con otras aplicaciones de SQL Server en la página de aplicaciones de Windows Server 2012, ejecute el programa de instalación de SQL Server para añadirlo a su instalación.

### <a name="sql-server-profiler"></a>SQL Server Profiler
 Aunque oficialmente no se use, SQL Server Profiler ofrece una forma sencilla de controlar las conexiones, ejecutar consultas MDX y otras operaciones del servidor. SQL Server Profiler está instalado de forma predeterminada. Puede encontrarlo con aplicaciones SQL Server en aplicaciones de Windows Server 2012.

### <a name="powershell"></a>PowerShell
 Puede utilizar comandos de PowerShell para realizar muchas tareas administrativas. Para obtener más información, vea [Analysis Services PowerShell](analysis-services-powershell.md) .

### <a name="community-and-third-party-tools"></a>Herramientas de la comunidad y de terceros
 Consulte la [página de codeplex Analysis Services](https://sqlsrvanalysissrvcs.codeplex.com/) para obtener ejemplos de código de la comunidad. Los [foros](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlanalysisservices) pueden ser útiles a la hora de buscar recomendaciones para herramientas de terceros que admiten Analysis Services.

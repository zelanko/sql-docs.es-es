---
title: Consultar las herramientas de diseño de informes, Diseñador de SQL Server Data Tools (SSRS) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- graphical query designer [Reporting Services]
- MDX query designer [Reporting Services]
- text-based query designer [Reporting Services]
- DMX [Reporting Services]
- query designers [Reporting Services]
- generic query designer See text-based query designer
- Reporting Services, query designers
- semantic queries [Reporting Services]
- Report Model Query Designer
ms.assetid: a8139a9d-4aeb-4e64-96f3-564edf60479f
caps.latest.revision: 35
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: ad3b9109d78523f8a273ce44e32ceab163bdf869
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109212"
---
# <a name="query-design-tools-in-report-designer-sql-server-data-tools-ssrs"></a>Herramientas de diseño de consultas en las herramientas de datos de SQL Server del Diseñador de informes (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ofrece varias herramientas de diseño de consultas que puede usar para crear consultas de conjuntos de datos en el Diseñador de consultas. El tipo de origen de datos con el que trabaje determinará la disponibilidad de un diseñador de consultas concreto. Además, algunos diseñadores de consultas ofrecen modos alternativos que le permiten elegir entre trabajar en modo visual o directamente en el idioma de la consulta. En este tema se presentan todas las herramientas y se describe el tipo de origen de datos que admite cada una de ellas. En esta sección se describen las siguientes herramientas:  
  
-   [Diseñador de consultas basado en texto](#Textbased)  
  
-   [Diseñador gráfico de consultas](#Graphical)  
  
-   [Diseñador de consultas de modelo de informe](#Model)  
  
-   [Diseñador de consultas MDX](#MDX)  
  
-   [Diseñador de consultas DMX](#DMX)  
  
-   [Diseñador de consultas de Sap NetWeaver BI](#SAPBW)  
  
-   [diseñador de consultas de Hyperion Essbase](#Hyperion)  
  
 Todas las herramientas de diseño de consultas se ejecutan en el entorno de diseño de datos de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] cuando se trabaja con una plantilla de proyecto del servidor de informes o del Asistente de proyectos de servidor de informes. Para obtener más información sobre cómo trabajar con diseñadores de consultas, vea [Reporting Services Query Designers](../reporting-services-query-designers.md).  
  
##  <a name="Textbased"></a> Diseñador de consultas basado en texto  
 El diseñador de consultas basado en texto es la herramienta predeterminada de creación de consultas para la mayoría de los orígenes de datos relacionales admitidos, incluidos [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], Oracle, Teradata, OLE DB, XML y ODBC. A diferencia del diseñador gráfico de consultas, esta herramienta de diseño de consultas no valida la sintaxis de las mismas durante su diseño. En la imagen siguiente se ilustra el diseñador de consultas basado en texto.  
  
 ![Diseñador de consultas genérico, para consultas de datos relacionales](../../analysis-services/media/rsqd-dsaw-sql-generic.gif "Diseñador de consultas genérico, para consultas de datos relacionales")  
  
 El diseñador de consultas basado en texto se recomienda para crear consultas complejas, usar procedimientos almacenados, realizar consultas en datos XML y escribir consultas dinámicas. Según el origen de datos, es posible que pueda alternar el botón **Editar como texto** de la barra de herramientas para cambiar entre el diseñador gráfico de consultas y el diseñador de consultas basado en texto. Para más información, vea [Interfaz de usuario del Diseñador de consultas basado en texto](../text-based-query-designer-user-interface.md).  
  
##  <a name="Graphical"></a> Diseñador gráfico de consultas  
 El diseñador gráfico de consultas se utiliza para crear o modificar consultas de [!INCLUDE[tsql](../../includes/tsql-md.md)] que se ejecutan con una base de datos relacional. Esta herramienta de diseño de consultas se utiliza en varios productos de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] y en otros componentes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Dependiendo del tipo de origen de datos, admite los modos Text, StoredProcedure y TableDirect. En la imagen siguiente se ilustra el diseñador gráfico de consultas.  
  
 ![Diseñador gráfico de consultas para consultas SQL](../media/rsqd-dsaw-sql.gif "Diseñador gráfico de consultas para consultas SQL")  
  
 Puede alternar el botón **Editar como texto** en la barra de herramientas para cambiar entre el diseñador gráfico de consultas y el diseñador de consultas basado en texto. Para más información, consulte [Graphical Query Designer User Interface](graphical-query-designer-user-interface.md).  
  
##  <a name="Model"></a> Diseñador de consultas de modelo de informe  
 El diseñador de consultas de modelo de informe se usa para crear o modificar las consultas que se ejecutan en un modelo de informe SMDL que se ha publicado en un servidor de informes. Los informes que se ejecutan en modelos admiten la exploración de datos click-through. La consulta determina la ruta de exploración de datos en tiempo de ejecución. En la imagen siguiente se ilustra el diseñador de consultas del Modelo de informes.  
  
 ![Interfaz de usuario del Diseñador de consultas de modelos semánticos](../media/rsqd-dsawmodel-smql.gif "Interfaz de usuario del Diseñador de consultas de modelos semánticos")  
  
 Para utilizar el diseñador de consultas de modelo de informe, debe definir un origen de datos que señale a un modelo publicado. Al definir un conjunto de datos para el origen de datos, puede abrir la consulta del conjunto de datos en el diseñador de consultas de modelo de informe. El diseñador de consultas de modelo de informe puede utilizarse en los modos gráfico o basado en texto. Puede alternar el botón **Editar como texto** en la barra de herramientas para cambiar entre el diseñador gráfico de consultas y el diseñador de consultas basado en texto. Para más información, consulte [Report Model Query Designer User Interface](report-model-query-designer-user-interface.md).  
  
##  <a name="MDX"></a> Diseñador de consultas MDX  
 El diseñador de consultas de expresiones multidimensionales (MDX) se usa para crear o modificar las consultas que se ejecutan en un origen de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] con cubos multidimensionales. En la imagen siguiente se muestra una ilustración del diseñador de consultas MDX después de haber definido la consulta y el filtro.  
  
 ![Diseñador de consultas MDX de Analysis Services, vista de diseño](../../analysis-services/media/rsqd-dsawas-mdx-designmode.gif "Diseñador de consultas MDX de Analysis Services, vista de diseño")  
  
 Para utilizar el diseñador de consultas MDX, debe definir un origen de datos que tenga un cubo de Analysis Services disponible que sea válido y se haya procesado. Al definir un conjunto de datos para el origen de datos, puede abrir la consulta en el diseñador de consultas MDX. Si es necesario, utilice los botones MDX y DMX en la barra de herramientas para cambiar entre los modos MDX y DMX. Para más información, consulte [Analysis Services MDX Query Designer User Interface](analysis-services-mdx-query-designer-user-interface.md).  
  
##  <a name="DMX"></a> Diseñador de consultas DMX  
 El diseñador de consultas de expresiones de predicción de minería de datos (DMX) se utiliza para crear o modificar consultas que se ejecutan en un origen de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] con modelos de minería de datos. La imagen siguiente proporciona una ilustración del diseñador de consultas DMX una vez seleccionadas las tablas de entrada y modelo.  
  
 ![Diseñador de consultas DMX de Analysis Services, vista de diseño](../media/rsqd-dsawas-dmx-designmode.gif "Diseñador de consultas DMX de Analysis Services, vista de diseño")  
  
 Para utilizar el diseñador de consultas DMX, debe definir un origen de datos que tenga disponible un modelo de minería de datos válido. Al definir un conjunto de datos para el origen de datos, puede abrir la consulta en el diseñador de consultas DMX. Si es necesario, utilice los botones MDX y DMX en la barra de herramientas para cambiar entre los modos MDX y DMX. Después de seleccionar el modelo, puede crear consultas de predicción de minería de datos que proporcionen datos para un informe. Para más información, consulte [Interfaz de usuario del Diseñador de consultas DMX de Analysis Services](analysis-services-dmx-query-designer-user-interface.md).  
  
##  <a name="SAPBW"></a> Diseñador de consultas de Sap NetWeaver BI  
 El diseñador de consultas de [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] se utiliza para recuperar los datos de una base de datos de [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] . Para usar este diseñador de consultas, debe tener un [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] origen de datos que tiene al menos un Infocubo, multisitio o consulta habilitada para Web definidos. En la imagen siguiente se ilustra el diseñador de consultas [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] .  
  
 ![Diseñador de consultas que usa MDX en modo de diseño](../media/rsqd-dssapbw-mdx-designmode.gif "Diseñador de consultas que usa MDX en modo de diseño")  
  
##  <a name="Hyperion"></a> diseñador de consultas de Hyperion Essbase  
 El diseñador de consultas de [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] se utiliza para recuperar los datos de las aplicaciones y bases de datos [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] . En la imagen siguiente se ilustra el diseñador de consultas [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] .  
  
 ![Diseñador de consultas para el origen de datos de Hyperion Essbase](../media/rsqd-dshyperionessbase-mdx-designmode.gif "Diseñador de consultas para el origen de datos de Hyperion Essbase")  
  
 Para utilizar este diseñador de consultas, debe tener un origen de datos de [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] que contenga al menos una base de datos. Para más información, consulte [SAP NetWeaver BI Query Designer User Interface](sap-netweaver-bi-query-designer-user-interface.md).  
  
## <a name="see-also"></a>Vea también  
 [Herramientas de Reporting Services](../tools/reporting-services-tools.md)   
 [Agregar datos a un informe &#40;el generador de informes SSRS&#41;](report-datasets-ssrs.md)   
 [Las conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Tutoriales de Reporting Services &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)   
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Crear un origen de datos incrustado o compartido &#40;SSRS&#41;](../create-an-embedded-or-shared-data-source-ssrs.md)  
  
  
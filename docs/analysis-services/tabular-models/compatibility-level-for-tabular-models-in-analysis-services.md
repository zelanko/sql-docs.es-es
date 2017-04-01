---
title: "Nivel de compatibilidad para modelos tabulares de Analysis Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.bidtoolset.versioncompat.f1"
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
caps.latest.revision: 27
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 27
---
# Nivel de compatibilidad para modelos tabulares de Analysis Services
  El *nivel de compatibilidad* de un modelo o una base de datos hace referencia a un conjunto de comportamientos específicos de la versión en el motor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Puede crear modelos en cualquier nivel de compatibilidad admitido para obtener los comportamientos de una versión concreta. Por ejemplo, los metadatos de objetos tabulares y de DirectQuery tienen implementaciones diferentes según la asignación del nivel de compatibilidad.  
  
 **SQL Server 2016 RTM (1200)**, también denominado nivel de compatibilidad 1200 para abreviar, es una novedad de SQL Server 2016 y solo se aplica a modelos tabulares.  Los modelos tabulares con un nivel de compatibilidad 1200 solo se ejecutarán en una instancia tabular de [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] .  
  
 Para crear o actualizar un modelo tabular, use SQL Server Data Tools (SSDT) y establezca la propiedad **Nivel de compatibilidad** al crear el proyecto o en el archivo **model.bim** después de crear el proyecto.  
  
> [!NOTE]  
>  Los modelos multidimensionales siguen una ruta de acceso de versión independiente en lo que respecta a los niveles de compatibilidad. Si los números son iguales, como es el caso de 1103, se trata de una mera coincidencia. Vea [Nivel de compatibilidad de una base de datos multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md) para obtener más información.  
  
## Niveles de compatibilidad admitidos para las bases de datos de modelo tabular  
 Analysis Services admite los niveles de compatibilidad siguientes, que son aplicables a modelos y bases de datos.  La versión de la herramienta que se usa para crear un modelo determina si existen niveles de compatibilidad más altos.  
  
||||  
|-|-|-|  
|nivel de compatibilidad|Versión del servidor|Versión de la herramienta de modelado|  
|1200|Solo se ejecuta en instancias de SQL Server 2016|[Solo SQL Server Data Tools para Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkID=690931) <sup>1</sup><br /><br /> [What's New in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md) describe la funcionalidad disponible en este nivel.|  
|1103|SQL Server 2016<br /><br /> SQL Server 2014<br /><br /> SQL Server 2012 SP1|[SQL Server Data Tools para Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkID=690931) <sup>2</sup><br /><br /> [SQL Server Data Tools para Business Intelligence (Visual Studio 2013)](https://www.microsoft.com/en-us/download/details.aspx?id=42313)<br /><br /> [SQL Server Data Tools para Business Intelligence (Visual Studio 2012)](http://www.microsoft.com/en-us/download/details.aspx?id=36843)|  
|1100|SQL Server 2016<br /><br /> SQL Server 2014<br /><br /> SQL Server 2012 SP1<br /><br /> SQL Server 2012|[SQL Server Data Tools para Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkID=690931) <sup>1</sup><br /><br /> [SQL Server Data Tools para Business Intelligence (Visual Studio 2013)](https://www.microsoft.com/en-us/download/details.aspx?id=42313)<br /><br /> [SQL Server Data Tools para Business Intelligence (Visual Studio 2012)](http://www.microsoft.com/en-us/download/details.aspx?id=36843)<br /><br /> Business Intelligence Development Studio (se ejecuta en el shell de Visual Studio 2010 y se instala con el programa de instalación de SQL Server)|  
  
 <sup>1</sup> Puede usar SQL Server Data Tools para Visual Studio 2015 para implementar un modelo tabular 1100 o 1103 en versiones anteriores de Analysis Services.  
  
 <sup>2</sup> Los niveles de compatibilidad 1100, 1103 y 1200 son válidos para los proyectos de modelos tabulares de SQL Server Data Tools para Visual Studio 2015, pero solo se puede implementar y ejecutar un modelo 1200 en una instancia de SQL Server 2016 de Analysis Services.  
  
## Establecer el nivel de compatibilidad al crear o actualizar un modelo tabular en SSDT  
 Al crear un proyecto de modelo tabular en SQL Server Data Tools (SSDT), puede especificar el nivel de compatibilidad en el cuadro de diálogo **New Tabular project options** (Opciones de nuevos proyectos tabulares):  
  
 ![ssas_tabularproject_compat1200](../../analysis-services/tabular-models/media/ssas-tabularproject-compat1200.jpg "ssas_tabularproject_compat1200")  
  
 También puede especificar un nivel de compatibilidad predeterminado si selecciona la opción **No volver a mostrar este mensaje** . Todos los proyectos posteriores usarán el nivel de compatibilidad que especificó. Puede cambiar el nivel de compatibilidad predeterminado en SSDT en **Herramientas** > **Opciones**.  
  
 Para actualizar un proyecto de modelo tabular, establezca la propiedad **Nivel de compatibilidad** en la ventana **Propiedades** del modelo en **SQL Server 2016 RTM (1200)**.  Consulte [Upgrade Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md) para obtener más información.  
  
> [!NOTE]  
>  Una forma de crear un modelo tabular consiste en basarlo en un libro Power Pivot importado. De forma predeterminada, Power BI Desktop crea modelos tabulares automáticamente en el nivel de compatibilidad 1200. Sin embargo, las versiones anteriores de los libros Power Pivot podrían estar en el nivel 1100. Cuando se usa un libro anterior, no olvide cambiar la propiedad **Nivel de compatibilidad** para actualizarlo.  
  
## Comprobar el nivel de compatibilidad para una base de datos en SSMS  
 En SSMS, haga clic con el botón derecho en el nombre de la base de datos > **Propiedades** > **propiedad Nivel de compatibilidad**.  
  
## Comprobar el nivel de compatibilidad admitido para un servidor en SSMS  
 En SSMS, haga clic con el botón derecho en el nombre del servidor > **Propiedades** > **Nivel de compatibilidad admitido**.  
  
 Esta propiedad especifica el máximo nivel de compatibilidad de una base de datos que se ejecutará en el servidor.  El nivel de compatibilidad admitido es de solo lectura y no se puede cambiar.  
  
## Vea también  
 [Nivel de compatibilidad de una base de datos multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Novedades de Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Importación desde PowerPivot &#40;SSAS Tabular&#41;](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md)   
 [Creación de un nuevo proyecto de modelo tabular &#40;Analysis Services&#41;](../../analysis-services/tabular-models/create-a-new-tabular-model-project-analysis-services.md)  
  
  
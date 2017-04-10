---
title: "Caracter&#237;sticas de Analysis Services compatibles con las ediciones de SQL Server 2016 | Microsoft Docs"
ms.custom: ""
ms.date: "09/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
  - "analysis-services/multidimensional-tabular"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f09d7be1-bd63-43f8-b91c-bf19166b4457
caps.latest.revision: 4
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 3
---
# Caracter&#237;sticas de Analysis Services compatibles con las ediciones de SQL Server 2016
Este tema proporciona información detallada de las características admitidas por las diversas ediciones de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
 La edición de evaluación de SQL Server está disponible durante un período de prueba de 180 días.  
  
 Para consultar las notas de la última versión, vea [SQL Server 2016 Release Notes](../sql-server/sql-server-2016-release-notes.md). Para obtener la información más reciente sobre novedades, consulte [Novedades de Analysis Services](../analysis-services/what-s-new-in-analysis-services.md).
    
 **Pruebe SQL Server 2016.**    
    
 > [![Descargar desde el centro de evaluación](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[Descargar SQL Server 2016 desde el centro de evaluación](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Máquina virtual de Azure pequeña](../analysis-services/media/azure-virtual-machine-small.png) **[Poner en marcha una máquina virtual con SQL Server 2016 ya instalado](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)**    
    
  
 Para conocer las características admitidas por las ediciones Evaluation y Developer, consulte SQL Server Enterprise Edition.
  
 Para navegar por la tabla para buscar una tecnología de SQL Server, haga clic en su vínculo: 
 
 -  [Analysis Services](#SSAS)  
  
-   [Modelo semántico BI (multidimensional)](#BIMD)  
  
-   [Modelo semántico BI (tabular)](#BIT)  
  
-   [PowerPivot para SharePoint](#PPSP)  
  
-   [Minería de datos](#DM)  
  
-   [Clientes de Business Intelligence](#BIC)  

##  <a name="SSAS"></a> Analysis Services  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express con herramientas|Express|Desarrollador|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Bases de datos compartidas escalables|Sí||||||Sí|  
|Copia de seguridad y restauración, y adjuntar y separar bases de datos|Sí|Sí|||||Sí|  
|Sincronizar bases de datos|Sí||||||Sí|  
|Instancias de clúster de conmutación por error de AlwaysOn|Sí<br /><br /> El número de nodos es el sistema operativo máximo|Sí<br /><br /> Compatibilidad con 2 nodos|||||Sí<br /><br /> El número de nodos es el sistema operativo máximo|  
|Programación (AMO, ADOMD.Net, OLEDB, XML/A, ASSL y TMSL)|Sí|Sí|||||Sí|  
  
##  <a name="BIMD"></a> Modelo semántico BI (multidimensional)  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express con herramientas|Express|Desarrollador|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Medidas de suma parcial|Sí|No <sup>1</sup>|||||Sí|  
|Jerarquías|Sí|Sí|||||Sí|  
|KPI|Sí|Sí|||||Sí|  
|Perspectivas|Sí||||||Sí|  
|Acciones|Sí|Sí|||||Sí|  
|Inteligencia de cuentas|Sí|Sí|||||Sí|  
|Inteligencia de tiempo|Sí|Sí|||||Sí|  
|Resúmenes personalizados|Sí|Sí|||||Sí|  
|Reescritura de cubos|Sí|Sí|||||Sí|  
|Reescritura de dimensiones|Sí||||||Sí|  
|Reescritura de celdas|Sí|Sí|||||Sí|  
|Obtención de detalles|Sí|Sí|||||Sí|  
|Tipos de jerarquías avanzadas (jerarquías primarios-secundarios y jerarquías desiguales)|Sí|Sí|||||Sí|  
|Dimensiones avanzadas (dimensiones de referencia, dimensiones de varios a varios)|Sí|Sí|||||Sí|  
|Medidas y dimensiones vinculadas|Sí|Sí  <sup>2</sup> |||||Sí|  
|Traducciones|Sí|Sí|||||Sí|  
|Agregaciones|Sí|Sí|||||Sí|  
|Varias particiones|Sí|Sí, hasta 3|||||Sí|  
|Almacenamiento en caché automático|Sí||||||Sí|  
|Ensamblados personalizados (procedimientos almacenados)|Sí|Sí|||||Sí|  
|Consultas MDX y scripts|Sí|Sí|||||Sí|  
|Consultas DAX|Sí|Sí|||||Sí|  
|Modelo de seguridad basada en roles|Sí|Sí|||||Sí|  
|Seguridad de dimensión y de nivel de celda|Sí|Sí|||||Sí|  
|Almacenamiento escalable de cadena|Sí|Sí|||||Sí|  
|Modelos de almacenamiento MOLAP, ROLAP y HOLAP|Sí|Sí|||||Sí|  
|Transporte XML comprimido y binario|Sí|Sí|||||Sí|  
|Procesamiento de modo de inserción|Sí||||||Sí|  
|Reescritura directa|Sí||||||Sí|  
|Expresiones de medida|Sí||||||Sí|  
  
 <sup>1</sup> La medida de suma parcial LastChild se admite en una edición estándar, a diferencia de otras medidas de suma parcial, como None, FirstChild, FirstNonEmpty, LastNonEmpty, AverageOfChildren y ByAccount. En todas las ediciones se admiten medidas de suma, como Sum, Count, Min y Max, y medidas de no suma (DistinctCount).  
  <sup>2</sup> La edición estándar admite la vinculación de medidas y dimensiones dentro de la misma base de datos, pero no de otras bases de datos o instancias.
   
##  <a name="BIT"></a> Modelo semántico BI (tabular)  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express con herramientas|Express|Desarrollador|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Jerarquías|Sí|Sí|||||Sí|  
|KPI|Sí|Sí|||||Sí|  
|Perspectivas|Sí||||||Sí|  
|Traducciones|Sí|Sí|||||Sí|  
|Cálculos de DAX, consultas de DAX, consultas MDX|Sí|Sí|||||Sí|  
|Seguridad de nivel de fila|Sí|Sí|||||Sí|  
|Varias particiones|Sí||||||Sí|  
|Modo de almacenamiento en memoria|Sí|Sí|||||Sí|  
|Modo de almacenamiento de DirectQuery|Sí||||||Sí|  
  
##  <a name="PPSP"></a> PowerPivot para SharePoint  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express con herramientas|Express|Desarrollador|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Integración de la granja de servidores de SharePoint según la arquitectura del servicio|Sí||||||Sí|  
|Informes de uso|Sí||||||Sí|  
|Reglas de seguimiento de estado|Sí||||||Sí|  
|Galería de PowerPivot|Sí||||||Sí|  
|Actualización de datos de PowerPivot|Sí||||||Sí|  
|Fuentes de distribución de datos de PowerPivot|Sí||||||Sí|  
  
##  <a name="DM"></a> Minería de datos  
  
|Nombre de la característica|Enterprise|Standard|Web|Express con Advanced Services|Express con herramientas|Express|Desarrollador|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Algoritmos estándar|Sí|Sí|||||Sí|  
|Herramientas de minería de datos (asistentes, editores y generadores de consultas)|Sí|Sí|||||Sí|  
|Validación cruzada|Sí||||||Sí|  
|Modelos de subconjuntos filtrados de datos de estructura de minería de datos|Sí||||||Sí|  
|Series temporales: mezcla personalizada entre métodos ARTXP y ARIMA|Sí||||||Sí|  
|Series horarias: predicción con nuevos datos|Sí||||||Sí|  
|Consultas de minería de datos simultáneas ilimitadas|Sí||||||Sí|  
|Configuración avanzada y opciones de optimización de algoritmos de minería de datos|Sí||||||Sí|  
|Compatibilidad con algoritmos de complemento|Sí||||||Sí|  
|Procesamiento de modelos en paralelo|Sí||||||Sí|  
|Series temporales: predicción de series cruzadas|Sí||||||Sí|  
|Atributos ilimitados para reglas de asociación|Sí||||||Sí|  
|Predicción de secuencias|Sí||||||Sí|  
|Varios destinos de predicción para Bayes naive, red neuronal y regresión logística|Sí||||||Sí|  
  
##  <a name="BIC"></a> Clientes de Business Intelligence  
 Las siguientes aplicaciones cliente de software están disponibles en el Centro de descarga de Microsoft y le ayudan a crear documentos de Business Intelligence que se ejecutan en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Si hospeda estos documentos en un entorno de servidor, use una edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] compatible con ese tipo de documento. En la siguiente tabla se indica qué edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiene las características de servidor necesarias para hospedar los documentos creados en estas aplicaciones cliente.  
  
|Nombre de la herramienta|Enterprise|Standard|Web|Express con Advanced Services|Express con herramientas|Express|Desarrollador|  
|---------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Complementos de minería de datos para Excel y Visio 2010 (.xlsx, .vsdx)|Sí|Sí|||||Sí|  
|[!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 2010 y 2013 (.xlsx)|Sí||||||Sí|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] (.xlsx)|Sí||||||Sí|  
  
> [!NOTE]  
>  1.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] es un complemento de Excel que sirve para crear libros con un modelo de datos.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] no depende de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], pero se necesita [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] para compartir y colaborar en libros de Excel con un modelo de datos en SharePoint. Esta función está disponible como parte de la edición [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise.  
>   
>      En Excel 2016, la función de PowerPivot está integrada, por lo que ya no necesita el complemento de PowerPivot.  
> 2.  En la tabla anterior se identifican las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] necesarias para habilitar estas herramientas de cliente, aunque dichas herramientas pueden obtener acceso a los datos hospedados en cualquier edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 ## Vea también  
 [Características compatibles con las ediciones de SQL Server 2016](Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
 [Especificaciones de producto para SQL Server 2016](../Topic/Product%20Specifications%20for%20SQL%20Server%202016.md)   
 [Instalación de SQL Server 2016](../database-engine/install-windows/installation-for-sql-server-2016.md)  


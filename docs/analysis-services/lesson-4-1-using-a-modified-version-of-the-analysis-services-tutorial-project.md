---
title: "Usar una versión modificada del análisis Services proyecto Tutorial | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 685aa217-de1b-4df2-bf22-095228c40775
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 10cb63369b23a19ecb126ee210de2a90ed114fc4
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-4-1---using-a-modified-version-of-the-analysis-services-tutorial-project"></a>Lección 4-1: uso de una versión modificada del proyecto Tutorial de Analysis Services
Las lecciones restantes de este tutorial se basan en una versión mejorada del proyecto Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que completó en las tres primeras lecciones. Se han agregado tablas y cálculos con nombre adicionales a la vista del origen de datos **Adventure Works DW 2012** , se han agregado más dimensiones al proyecto y estas nuevas dimensiones se han agregado al cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Además, se ha agregado un segundo grupo de medidas, que contiene medidas de una segunda tabla de hechos. Este proyecto mejorado le permitirá continuar aprendiendo a agregar funciones adicionales a la aplicación de Business Intelligence sin necesidad de tener que repetir las técnicas ya aprendidas.  
  
Para poder continuar con el tutorial, debe descargar, extraer, cargar y procesar la versión mejorada del proyecto Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  Siga las instrucciones de esta lección para asegurarse de que ha realizado todos los pasos.  
  
## <a name="downloading-and-extracting-the-project-file"></a>Descargar y extraer el archivo de proyecto  
  
1.  [Haga clic aquí](http://go.microsoft.com/fwlink/?LinkID=221866) para ir a la página de descarga que proporciona los proyectos de ejemplo relacionados con este tutorial. Los proyectos del tutorial se incluyen en la descarga de **Tutorial de Analysis Services SQL Server 2012** .  
  
2.  Haga clic en **Tutorial de Analysis Services de SQL Server 2012** para descargar el paquete que contiene los proyectos para este tutorial.  
  
    De forma predeterminada, se guarda un archivo .zip en la carpeta Descargas. Debe mover el archivo .zip a una ubicación que tenga una ruta de acceso más corta (por ejemplo, cree una carpeta C:\Tutoriales para almacenar los archivos).  Después puede extraer los archivos contenidos en el archivo .zip. Si intentar descomprimir los archivos desde la carpeta Descargas, que tiene una ruta de acceso más larga, solo obtendrá la lección 1.  
  
3.  Cree una subcarpeta en la unidad raíz, o cerca de ella, por ejemplo C:\Tutorial.  
  
4.  Mueva el archivo **Analysis Services Tutorial SQL Server 2012.zip** a la subcarpeta.  
  
5.  Haga clic con el botón derecho en el archivo y seleccione **Extraer todo**.  
  
6.  Vaya a la carpeta **Lesson 4 Start** para buscar el archivo **Analysis Services Tutorial.sln** .  
  
## <a name="loading-and-processing-the-enhanced-project"></a>Cargar y procesar el proyecto mejorado  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], en el menú **Archivo** , haga clic en **Cerrar solución** para cerrar los archivos que no vaya a usar.  
  
2.  En el menú **Archivo** , seleccione **Abrir**y haga clic en **Proyecto o solución**.  
  
3.  Vaya a la ubicación donde extrajo los archivos del proyecto de tutorial.  
  
    Busque la carpeta denominada **Lesson 4 Start**y haga doble clic en Analysis Services Tutorial.sln.  
  
4.  Implemente la versión mejorada del proyecto Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en la instancia local de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], o en otra instancia, y compruebe que el proceso finaliza correctamente.  
  
## <a name="understanding-the-enhancements-to-the-project"></a>Comprender las mejoras realizadas en el proyecto  
La versión mejorada del proyecto es distinta de la versión del proyecto Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que completó en las tres primeras lecciones. Las diferencias se describen en las siguientes secciones: Revise esta información antes de continuar con las lecciones restantes del tutorial.  
  
### <a name="data-source-view"></a>Vista del origen de datos  
La vista del origen de datos del proyecto mejorado contiene una tabla de hechos adicional y cuatro tablas de dimensiones adicionales de la base de datos [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] .  
  
Observe que, con diez tablas en la vista del origen de datos, el diagrama <All Tables> empieza a estar demasiado lleno. Esto dificulta la comprensión de las relaciones entre las tablas y la localización de tablas específicas. Para resolver este problema, las tablas están organizadas en dos diagramas lógicos, el diagrama **Internet Sales** y el diagrama **Reseller Sales** . Estos diagramas están organizados cada uno en una única tabla de hechos. Crear diagramas lógicos permite ver y utilizar un subconjunto específico de tablas de la vista del origen de datos en lugar de ver siempre todas las tablas y sus relaciones en un único diagrama.  
  
#### <a name="internet-sales-diagram"></a>Diagrama Internet Sales  
El diagrama **Internet Sales** contiene las tablas que están relacionadas con la venta directa de productos de [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] a los clientes a través de Internet. Las tablas del diagrama son las cuatro tablas de dimensiones y la tabla de hechos que agregó a la vista del origen de datos **Adventure Works DW 2012** en la Lección 1. Estas tablas son las siguientes:  
  
-   **Geografía**  
  
-   **Customer**  
  
-   **Date**  
  
-   **Product**  
  
-   **InternetSales**  
  
#### <a name="reseller-sales-diagram"></a>Diagrama Reseller Sales  
El diagrama **Reseller Sales** contiene las tablas relacionadas con la venta de productos de [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] realizadas por los distribuidores. Este diagrama contiene las siete tablas de dimensiones siguientes y una tabla de hechos de la base de datos [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] :  
  
-   **Reseller**  
  
-   **Promoción**  
  
-   **SalesTerritory**  
  
-   **Geografía**  
  
-   **Date**  
  
-   **Product**  
  
-   **Employee**  
  
-   **ResellerSales**  
  
Como puede observar, las tablas **DimGeography**, **DimDate**y **DimProduct** se usan tanto en el diagrama **Internet Sales** como en el diagrama **Reseller Sales** . Las tablas de dimensiones pueden vincularse a varias tablas de hechos.  
  
### <a name="database-and-cube-dimensions"></a>Dimensiones de cubo y base de datos  
El proyecto Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] contiene cinco dimensiones de base de datos nuevas, y el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] contiene las mismas cinco dimensiones que las dimensiones del cubo. Estas dimensiones se han definido de modo que contengan jerarquías de usuario y atributos que se modificaron mediante cálculos con nombre, claves de miembro de composición y carpetas para mostrar. Las nuevas dimensiones se describen en la siguiente lista.  
  
Dimensión Reseller  
La dimensión Reseller se basa en la tabla **Reseller** de la vista del origen de datos **Adventure Works DW 2012** .  
  
Dimensión Promotion  
La dimensión Promotion se basa en la tabla **Promotion** de la vista del origen de datos **Adventure Works DW 2012** .  
  
Dimensión Sales Territory  
La dimensión Sales Territory se basa en la tabla **SalesTerritory** de la vista del origen de datos **Adventure Works DW 2012** .  
  
Dimensión Employee  
La dimensión Employee se basa en la tabla **Employee** de la vista del origen de datos **Adventure Works DW 2012** .  
  
Dimensión Geography  
La dimensión Geography se basa en la tabla **Geography** de la vista del origen de datos **Adventure Works DW 2012** .  
  
#### <a name="analysis-services-cube"></a>Cubo Analysis Services  
El cubo **Tutorial de Analysis Services** contiene ahora dos grupos de medida: el grupo de medida original basado en la tabla **InternetSales** y un segundo grupo de medida basado en la tabla **ResellerSales** de la vista del origen de datos **Adventure Works DW 2012** .  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Definir propiedades de atributo primario en una jerarquía de elementos primarios y secundarios](../analysis-services/lesson-4-2-defining-parent-attribute-properties-in-a-parent-child-hierarchy.md)  
  
## <a name="see-also"></a>Vea también  
[Implementar un proyecto de Analysis Services](../analysis-services/lesson-2-5-deploying-an-analysis-services-project.md)  
  


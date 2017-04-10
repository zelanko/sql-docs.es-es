---
title: "Lecci&#243;n 1: Crear un nuevo proyecto de modelo tabular | Microsoft Docs"
ms.custom: ""
ms.date: "03/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 0d2eb34d-78c8-41ff-b92d-49b62c16b2ac
caps.latest.revision: 33
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 28
---
# Lecci&#243;n 1: Crear un nuevo proyecto de modelo tabular
En esta lección, creará un nuevo proyecto de modelo tabular en blanco en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Una vez creado el nuevo proyecto, puede comenzar a agregar datos usando el Asistente para la importación de tablas. Además de crear un nuevo proyecto, esta lección incluye también una breve introducción al entorno de creación de modelos tabulares en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
Para obtener más información sobre los diferentes tipos de proyectos de modelos tabulares, vea [Proyectos de modelos tabulares &#40;SSAS tabular&#41;](../analysis-services/tabular-models/tabular-model-projects-ssas-tabular.md). Para obtener más información sobre el entorno de creación de modelos tabulares, vea [Diseñador de modelos tabulares &#40;SSAS&#41;](../analysis-services/tabular-models/tabular-model-designer-ssas.md).  
  
Tiempo estimado para completar esta lección: **10 minutos**  
  
## Requisitos previos  
Este tema es la primera lección de un tutorial de creación de modelos tabulares. Para completar esta lección, debe tener la base de datos AdventureWorksDW instalada en una instancia de SQL Server. Para obtener más información, vea [Creación de modelos tabulares &#40;tutorial de Adventure Works&#41;](../analysis-services/tabular-modeling-adventure-works-tutorial.md).  
  
## Crear un nuevo proyecto de modelo tabular  
  
#### Para crear un nuevo proyecto de modelo tabular  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], en el menú **Archivo** , haga clic en **Nuevo**y, a continuación, en **Proyecto**.  
  
2.  En el cuadro de diálogo **Nuevo proyecto**, en **Instalado**, haga clic en **Business Intelligence**, en **Analysis Services** y en **Proyecto tabular de Analysis Services**.  
  
3.  En **Nombre**, escriba **Modelo tabular de ventas por Internet de AW** y especifique una ubicación para los archivos del proyecto.  
  
    De forma predeterminada, el **Nombre de la solución** será el mismo que el nombre del proyecto, pero puede especificar un nombre de solución diferente.  
  
4.  Haga clic en **Aceptar**.  
  
5.  En el cuadro de diálogo **Diseñador de modelos tabulares**, en **Servidor del área de trabajo**, escriba el nombre de una instancia de SQL Server 2016 Analysis Services en la que tenga permisos de administrador del servidor y haga clic en **Prueba de conexión**.  
  
    La instancia del servidor del área de trabajo que especifique hospedará una base de datos de modelo tabular con el mismo nombre que el proyecto durante la creación.   
      
6.  En **Nivel de compatibilidad**, compruebe que está seleccionado **SQL Server 2016 (1200)** y haga clic en **Aceptar**.   
      
    Si no ve SQL Server 2016 (1200) en el cuadro de lista Nivel de compatibilidad, no está usando la versión más reciente de SQL Server Data Tools. Para obtener la versión más reciente, vea [Instalar SQL Server Data Tools](https://msdn.microsoft.com/hh500335(v=vs.103).aspx).   
      
    Solo se recomienda seleccionar un nivel de compatibilidad anterior si tiene intención de implementar el modelo tabular completado en otra instancia de Analysis Services que ejecute SQL Server 2012 o SQL Server 2014. Para obtener más información, vea [Nivel de compatibilidad](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).   
  
## Descripción del entorno de creación de modelos tabulares con las herramientas de datos de SQL Server  
Ahora que ha creado un nuevo proyecto de modelo tabular, dedique un momento a examinar el entorno de creación de modelos tabulares de [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] (Visual Studio 2010 o posterior).  
  
Después de crear el proyecto, este se abre en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Aparecerá un modelo vacío en el diseñador de modelos y el archivo **Model.bim** se seleccionará en la ventana **Explorador de soluciones**. Cuando agregue datos, aparecerán tablas y columnas en el diseñador. Si no ve el diseñador (la ventana vacía con la pestaña Model.bim), en el **Explorador de soluciones**, en **Modelo tabular de ventas por Internet de AW**, haga doble clic en el archivo **Model.bim**.  
  
Puede ver las propiedades básicas del proyecto en la ventana **Propiedades**. En el **Explorador de soluciones**, haga clic en **Modelo tabular de ventas por Internet de AW**. Observe que en la ventana **Propiedades**, en **Archivo de proyecto**, aparece **Modelo tabular de ventas por Internet de AW.smproj**. Este es el nombre de archivo del proyecto. En **Carpeta del proyecto**, verá la ubicación del archivo del proyecto.  
  
En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto **Modelo tabular de ventas por Internet de AW** y haga clic en **Propiedades**. Aparece el cuadro de diálogo **Páginas de propiedades del Modelo tabular de ventas por Internet de AW**. Estas son las propiedades avanzadas del proyecto. Establecerá alguna de estas propiedades más adelante cuando esté preparado para implementar el modelo.  
  
Ahora, examinemos las propiedades del modelo. En el **Explorador de soluciones**, haga clic en **Model.bim**. En la ventana **Propiedades** verá ahora las propiedades del modelo, de las cuales la más importante es **Modo DirectQuery**. Esta propiedad especifica si el modelo se va a implementar en modo de almacenamiento en memoria (desactivada) o en modo DirectQuery (activada). En este tutorial, creará e implementará el modelo en modo de almacenamiento en memoria.  
  
Cuando crea un modelo nuevo, algunas propiedades del modelo se establecen automáticamente según la configuración del modelo de datos, que puede especificarse en Herramientas\cuadro de diálogo Opciones. Las propiedades Copia de seguridad de datos, Retención de área de trabajo y Servidor del área de trabajo especifican cómo y dónde se realiza una copia de seguridad, se conserva en memoria y se crea la base de datos del área de trabajo (la base de datos de creación del modelo). Puede cambiar esta configuración más adelante si es necesario, pero de momento deje estas propiedades tal como están.  
  
Cuando instaló [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], se agregaron varios elementos de menú nuevos al entorno de Visual Studio. Examinemos los nuevos elementos de menú que son específicos de la creación de modelos tabulares. Haga clic en el menú **Modelo**. Desde aquí, puede iniciar el Asistente para la importación de tablas, ver y editar conexiones existentes, actualizar los datos del área de trabajo, examinar el modelo en [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel con la característica Analizar de Excel, crear perspectivas y roles, seleccionar la vista del modelo y definir opciones de cálculo.  
  
Haga clic en el menú **Tabla**. Aquí puede crear y administrar las relaciones entre tablas, crear y administrar tablas, especificar la configuración de las tablas de datos, crear particiones y editar las propiedades de tabla.  
  
Haga clic en el menú **Columna**. Aquí puede agregar y eliminar columnas de una tabla, inmovilizar columnas y especificar el criterio de ordenación. También puede utilizar la característica de autosuma para crear una medida de agregación estándar para una columna seleccionada. Otros botones de la barra de herramientas proporcionan acceso rápido a características y comandos usados con frecuencia.  
  
Examine algunos de los cuadros de diálogo y ubicaciones de las distintas características específicas de la creación de modelos tabulares. Aunque algunos elementos aún no estén activos, puede hacerse una idea de cómo es el entorno de creación de modelos tabulares.  
  
## Pasos siguientes  
Para continuar este tutorial, vaya a la lección siguiente: [Lección 2: Agregar datos](../analysis-services/lesson-2-add-data.md).  
  
  
  

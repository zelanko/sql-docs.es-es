---
title: "Lección 1: Crear un nuevo proyecto de modelo Tabular | Documentos de Microsoft"
ms.custom: 
ms.date: 03/27/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 0d2eb34d-78c8-41ff-b92d-49b62c16b2ac
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: fe1c808d84bac0c14e1cf46c4613464e04bbea0c
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
---
# <a name="lesson-1-create-a-new-tabular-model-project"></a>Lección 1: Crear un nuevo proyecto de modelo tabular
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

En esta lección, creará un nuevo proyecto de modelo tabular en blanco en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Una vez creado el nuevo proyecto, puede comenzar a agregar datos usando el Asistente para la importación de tablas. En esta lección también se ofrece una breve introducción a entorno de SSDT de creación de modelos tabulares.  
  
Tiempo estimado para completar esta lección: **10 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema es la primera lección de un tutorial de creación de modelos tabulares. Para completar esta lección, debe tener la base de datos de ejemplo AdventureWorksDW instalada en una instancia de SQL Server. Para obtener más información, consulte [creación de modelos tabulares &#40; Tutorial de Adventure Works &#41; ](../analysis-services/tabular-modeling-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Crear un nuevo proyecto de modelo tabular  
  
#### <a name="to-create-a-new-tabular-model-project"></a>Para crear un nuevo proyecto de modelo tabular  
  
1.  En SSDT, en la **archivo** menú, haga clic en **New** > **proyecto**.  
  
2.  En el **nuevo proyecto** cuadro de diálogo, expanda **instalado** > **Business Intelligence** > **Analysis Services**y, a continuación, haga clic en **proyecto Tabular de Analysis Services**.  
  
3.  En **nombre**, tipo **AW Internet Sales**y, a continuación, especifique una ubicación para los archivos de proyecto.  
  
    De forma predeterminada, el **Nombre de la solución** será el mismo que el nombre del proyecto, pero puede especificar un nombre de solución diferente.  
  
4.  Haga clic en **Aceptar**.  
  
5.  En el **Diseñador de modelos tabulares** cuadro de diálogo, seleccione **área de trabajo integrado**.  
  
    El área de trabajo va a hospedar una base de datos de modelo tabular con el mismo nombre que el proyecto durante la creación del modelo. Área de trabajo integrado significa que SSDT usará una instancia integrada, lo que elimina la necesidad de instalar una instancia de servidor de Analysis Services independiente solo para la creación de modelos. Para obtener más información, consulte [base de datos del área de trabajo](../analysis-services/tabular-models/workspace-database-ssas-tabular.md).
      
6.  En **Nivel de compatibilidad**, compruebe que está seleccionado **SQL Server 2016 (1200)** y haga clic en **Aceptar**.   
 
    ![as-tabular-lesson1-tmd](../analysis-services/media/as-tabular-lesson1-tmd.png)
      
    Si no ve el SQL Server 2016 RTM (1200) en el cuadro de lista de nivel de compatibilidad, que no está utilizando la versión más reciente de SQL Server Data Tools. Para obtener la versión más reciente, vea [Instalar SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  

    Si usa la versión más reciente de SSDT, también puede elegir SQL Server 2017 (1400). Sin embargo, para realizar la lección 13: implementar, necesitará un servidor SQL Server 2017 o Azure para implementar en.
      
    Al seleccionar un nivel de compatibilidad anterior solo se recomienda si tiene intención de implementar el modelo completado tabular a otra instancia de Analysis Services ejecuta una versión anterior de SQL Server. Área de trabajo integrado no se admite para los niveles de compatibilidad anterior. Para obtener más información, vea [Nivel de compatibilidad](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).   
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a>Descripción del entorno de creación de modelos tabulares de SSDT  
Ahora que ha creado un nuevo proyecto de modelo tabular, dedique un momento a examinar el entorno de SSDT de creación de modelos tabulares.  
  
Una vez creado el proyecto, se abre en SSDT. En el lado derecho, en **Explorador de modelos tabulares**, verá una vista de árbol de los objetos en el modelo. Puesto que aún no ha importado datos, las carpetas estará vacías. Puede hacer clic una carpeta de objeto para llevar a cabo acciones, similares a la barra de menús. Paso a paso a través de este tutorial, usará el Explorador de modelos tabulares para navegar por los distintos objetos en el proyecto de modelos.

![como-tabular-lesson1-tiempo](../analysis-services/media/as-tabular-lesson1-tme.png)

Haga clic en el **el Explorador de soluciones** ficha. En este caso, verá la **Model.bim** archivo. Si no ve la ventana del diseñador a la izquierda (la ventana vacía con la pestaña Model.bim), en **el Explorador de soluciones**, en **AW Internet Sales proyecto**, haga doble clic en el **Model.bim** archivo. El archivo Model.bim contiene todos los metadatos para el proyecto de modelos. 

![as-tabular-lesson1-se](../analysis-services/media/as-tabular-lesson1-se.png)
  
Echemos un vistazo a las propiedades del modelo. Haga clic en **Model.bim**. En el **propiedades** ventana, verá el [propiedades de los modelos](../analysis-services/tabular-models/model-properties-ssas-tabular.md), más importante que es el **Directquerymode** propiedad. Esta propiedad especifica si el modelo se va a implementar en modo de almacenamiento en memoria (desactivada) o en modo DirectQuery (activada). En este tutorial, creará e implementará el modelo en modo de almacenamiento en memoria.

![as-tabular-lesson1-properties](../analysis-services/media/as-tabular-lesson1-properties.png)
  
Cuando se crea un nuevo modelo, algunas propiedades del modelo se establecen automáticamente según la configuración de modelado de datos que se pueden especificar en el **herramientas** > **opciones** cuadro de diálogo. Las propiedades Copia de seguridad de datos, Retención de área de trabajo y Servidor del área de trabajo especifican cómo y dónde se realiza una copia de seguridad, se conserva en memoria y se crea la base de datos del área de trabajo (la base de datos de creación del modelo). Puede cambiar esta configuración más adelante si es necesario, pero de momento deje estas propiedades tal como están.  

En **el Explorador de soluciones**, haga clic en **AW Internet Sales** (proyecto) y, a continuación, haga clic en **propiedades**. El **páginas de propiedades de ventas de Internet de AW** aparece el cuadro de diálogo. Estos son los avanzados [propiedades del proyecto](../analysis-services/tabular-models/project-properties-ssas-tabular.md). Establecerá alguna de estas propiedades más adelante cuando esté preparado para implementar el modelo.  
  
Al instalar SSDT, se agregaron varios elementos de menú nuevos al entorno de Visual Studio. Echemos un vistazo a los específicos para la creación de modelos tabulares. Haga clic en el menú **Modelo** . Desde aquí, puede iniciar al Asistente para importación de tablas, ver y modificar las conexiones existentes, actualizar los datos del área de trabajo, examinar el modelo en Excel con la característica analizar en Excel, crear perspectivas y roles, seleccione la vista del modelo y establecer las opciones de cálculo.  
  
Haga clic en el menú **Tabla** . Aquí puede crear y administrar las relaciones entre tablas, crear y administrar tablas, especificar la configuración de las tablas de datos, crear particiones y editar las propiedades de tabla.  
  
Haga clic en el menú **Columna** . Aquí puede agregar y eliminar columnas de una tabla, inmovilizar columnas y especificar el criterio de ordenación. También puede utilizar la característica de autosuma para crear una medida de agregación estándar para una columna seleccionada. Otros botones de la barra de herramientas proporcionan acceso rápido a características y comandos usados con frecuencia.  
  
Examine algunos de los cuadros de diálogo y ubicaciones de las distintas características específicas de la creación de modelos tabulares. Aunque algunos elementos aún no estén activos, puede hacerse una idea de cómo es el entorno de creación de modelos tabulares.  


## <a name="additional-resources"></a>Recursos adicionales
Para obtener más información sobre los diferentes tipos de proyectos de modelos tabulares, vea [proyectos de modelos tabulares](../analysis-services/tabular-models/tabular-model-projects-ssas-tabular.md). Para obtener más información sobre el entorno de creación de modelos tabulares, vea [Diseñador de modelos tabulares ](../analysis-services/tabular-models/tabular-model-designer-ssas.md).  
  

## <a name="whats-next"></a>¿Qué sigue?
Vaya a la siguiente lección: [lección 2: agregar datos](../analysis-services/lesson-2-add-data.md).

  
  
  

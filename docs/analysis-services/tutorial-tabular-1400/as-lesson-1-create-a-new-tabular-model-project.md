---
title: 'Lección de Analysis Services tutorial 1: crear un nuevo proyecto de modelo tabular | Documentos de Microsoft'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 403e6d04d339e3126afe964bd919304d04295c0b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34044199"
---
# <a name="create-a-tabular-model-project"></a>Crear un proyecto de modelo tabular

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección, use Visual Studio con SQL Server Data Tools (SSDT) o Visual Studio de 2017 con Microsoft Analysis Services proyectos VSIX para crear un nuevo proyecto de modelo tabular en el nivel de compatibilidad de 1400. Cuando se crea el nuevo proyecto, podrá empezar a agregar datos y crear el modelo. En esta lección también se ofrece una breve introducción a entorno de Visual Studio de creación de modelos tabulares.  
  
Tiempo estimado para completar esta lección: **10 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos

Este artículo es la primera lección de un tutorial de creación de modelos tabulares. Para completar esta lección, hay varios requisitos previos que debe tener en contexto. Para obtener más información, consulte [Analysis Services - tutorial de Adventure Works](../tutorial-tabular-1400/as-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Crear un nuevo proyecto de modelo tabular  
  
#### <a name="to-create-a-new-tabular-model-project"></a>Para crear un nuevo proyecto de modelo tabular  
  
1.  En Visual Studio, en el **archivo** menú, haga clic en **New** > **proyecto**.  
  
2.  En el **nuevo proyecto** cuadro de diálogo, expanda **instalado** > **Business Intelligence** > **Analysis Services**y, a continuación, haga clic en **proyecto Tabular de Analysis Services**.  
  
3.  En **nombre**, tipo **AW Internet Sales**y, a continuación, especifique una ubicación para los archivos de proyecto.  
  
    De forma predeterminada, **nombre de la solución** es el mismo que el nombre del proyecto; sin embargo, puede escribir un nombre de solución diferente.  
  
4.  Haga clic en **Aceptar**.  
  
5.  En el **Diseñador de modelos tabulares** cuadro de diálogo, seleccione **área de trabajo integrado**.  
  
    El área de trabajo hospeda una base de datos de modelo tabular con el mismo nombre que el proyecto durante la creación del modelo. Área de trabajo integrado significa que Visual Studio usa una instancia integrada, lo que elimina la necesidad de instalar una instancia de servidor de Analysis Services independiente solo para la creación de modelos.
      
6.  En **nivel de compatibilidad**, seleccione **2017 / Azure Analysis Services de SQL Server (1400)**.   
 
    ![tmd como lesson1](../tutorial-tabular-1400/media/as-lesson1-tmd.png)
      
    Si no ve SQL Server 2017 / Azure Analysis Services (1400) en el cuadro de lista de nivel de compatibilidad, que no está utilizando la versión más reciente de SQL Server Data Tools. Para obtener la versión más reciente, vea [Instalar SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  
      
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a>Descripción del entorno de creación de modelos tabulares de SSDT  

Ahora que ha creado un nuevo proyecto de modelo tabular, dedique un momento a examinar el entorno de Visual Studio de creación de modelos tabulares.  
  
Una vez creado el proyecto, se abre en Visual Studio. En el lado derecho, en **Explorador de modelos tabulares**, verá una vista de árbol de los objetos en el modelo. Puesto que aún no ha importado datos, las carpetas están vacías. Puede hacer clic una carpeta de objeto para llevar a cabo acciones, similares a la barra de menús. Paso a paso a través de este tutorial, utilice el Explorador de modelos tabulares para navegar por los distintos objetos en el proyecto de modelos.

![tiempo como lesson1](../tutorial-tabular-1400/media/as-lesson1-tme.png)

Haga clic en el **el Explorador de soluciones** ficha. En este caso, verá la **Model.bim** archivo. Si no ve la ventana del diseñador a la izquierda (la ventana vacía con la pestaña Model.bim), en **el Explorador de soluciones**, en **AW Internet Sales proyecto**, haga doble clic en el **Model.bim** archivo. El archivo Model.bim contiene los metadatos para el proyecto de modelos. 

![como-lesson1-se](../tutorial-tabular-1400/media/as-lesson1-se.png)
  
Haga clic en **Model.bim**. En el **propiedades** ventana, verá las propiedades del modelo, que es más importantes la **Directquerymode** propiedad. Esta propiedad especifica si el modelo se implementa en modo In-Memory (Off) o en modo de DirectQuery (activado). En este tutorial, se e implementará el modelo en el modo en memoria.

![propiedades como lesson1](../tutorial-tabular-1400/media/as-lesson1-properties.png)
  
Al crear un proyecto de modelo, algunas propiedades del modelo se establecen automáticamente según la configuración de modelado de datos que se pueden especificar en el **herramientas** menú > **opciones** cuadro de diálogo. Las propiedades Copia de seguridad de datos, Retención de área de trabajo y Servidor del área de trabajo especifican cómo y dónde se realiza una copia de seguridad, se conserva en memoria y se crea la base de datos del área de trabajo (la base de datos de creación del modelo). Puede cambiar esta configuración más adelante si es necesario, pero por ahora, déjelo estas propiedades tal como están.  

En **el Explorador de soluciones**, haga clic en **AW Internet Sales** (proyecto) y, a continuación, haga clic en **propiedades**. El **páginas de propiedades de ventas de Internet de AW** aparece el cuadro de diálogo. Establece algunas de estas propiedades más adelante al implementar el modelo.  
  
Al instalar SSDT, se agregaron varios elementos de menú nuevos al entorno de Visual Studio. Haga clic en el **modelo** menú. Desde aquí, puede importar datos, actualizar los datos del área de trabajo, examinar el modelo en Excel, crear perspectivas y roles, seleccione la vista de modelo y establecer las opciones de cálculo. Haga clic en el **tabla** menú. Desde aquí, puede crear y administrar relaciones, especificar la configuración de la tabla de fecha, crear particiones y editar propiedades de tabla. Si hace clic en el **columna** menú, puede agregar y eliminar columnas de una tabla, Inmovilizar columnas y especificar el criterio de ordenación. SSDT también agrega algunos botones a la barra. Más útil es la característica de Autosuma para crear una medida de agregación estándar para una columna seleccionada. Otros botones de la barra de herramientas proporcionan acceso rápido a características y comandos usados con frecuencia.  
  
Examine algunos de los cuadros de diálogo y ubicaciones de las distintas características específicas de la creación de modelos tabulares. Aunque algunos elementos aún no están activos, puede obtener una idea del entorno de creación de modelos tabulares.  
  

## <a name="whats-next"></a>¿Qué sigue?

[Lección 2: Obtener datos](../tutorial-tabular-1400/as-lesson-2-get-data.md).

  
  
  

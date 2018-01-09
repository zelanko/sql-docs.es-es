---
title: "Importar un proyecto de minería de datos mediante el Asistente para la importación de Analysis Services | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 62bc9fc5-c6ff-4517-b598-d92df76743a2
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5f7a99df396ecef55f0ba6a4529416354cdccda1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="import-a-data-mining-project-using-the-analysis-services-import-wizard"></a>Cantidad un proyecto de minería de datos mediante el Asistente para la importación de Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Este tema describe cómo crear un nuevo proyecto de minería de datos importando los metadatos de un proyecto de minería de datos existente en otro servidor, mediante la plantilla, **importar desde el proyecto de servidor (Multidimensional y minería de datos)**, en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="import-data-sources-mining-structures-and-mining-models-from-an-existing-data-mining-project"></a>Importar los orígenes de datos, estructuras de minería de datos y modelos de minería de datos de un proyecto de minería de datos existente  
 Al usar la plantilla de proyecto **Importar del servidor (multidimensional y minería de datos)**, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] crea un nuevo proyecto de minería de datos y después copia los metadatos del proyecto especificado de minería de datos. El nuevo proyecto contiene los mismos orígenes de datos, vistas del origen de datos, estructuras de minería de datos y modelos de minería de datos que la base de datos de los que los importó. Sin embargo, el proyecto no se puede utilizar hasta que se haya actualizado ciertas propiedades y haya procesado los objetos según se indica:  
  
-   Los propios datos no se copian del servidor de origen al nuevo proyecto de minería de datos, solo se importan las definiciones de los orígenes de datos y las vistas del origen de datos. Por consiguiente, cuando el proceso de importación haya finalizado y los objetos se hayan creado, debe rellenar los objetos con datos entrenando los modelos dependientes y las estructuras de minería de datos. Puede utilizar el comando **Procesar todo** del Diseñador de minería de datos para entrenar los modelos y las estructuras.  
  
-   Si importa un proyecto creado en una versión anterior de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], el origen de datos puede utilizar proveedores que no estén instalados en el servidor en el que vaya a importar el proyecto. Si surgen errores al procesar las estructuras de minería de datos importadas, haga clic con el botón derecho en cada origen de datos y seleccione **Abrir diseñador** para modificar la cadena de conexión y revisar las propiedades del proveedor.  
  
     En este momento, puede que también deba comprobar que la cuenta que utiliza para procesar los objetos de minería de datos o los modelos de minería de datos de consulta tengan los permisos necesarios en el origen de datos.  
  
-   De forma predeterminada, cuando se importa un proyecto, la base de datos del área de trabajo se establece en el host local, o cualquier instancia predeterminada se configura como **Servidor de destino predeterminado** en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para establecer esta propiedad, en el menú **Opciones** , seleccione **Diseñadores de Business Intelligence**, seleccione **Analysis Services**y, a continuación, seleccione **General**.  
  
     Tenga en cuenta que, en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], hay otra opción distinta que puede establecer para configurar el servidor de implementación predeterminado para los proyectos de modelos tabulares de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . El valor, **Servidor de implementación predeterminado**, determina la base de datos predeterminada del área de trabajo de los proyectos de modelos tabulares. No puede utilizar las instancias que admitan modelos tabulares para proyectos de minería de datos  
  
     Si no puede cambiar la base de datos predeterminada de implementación para utilizar una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se ejecuta en modo MDX o de minería de datos, siempre puede especificar la base de datos de implementación mediante el cuadro de diálogo **Propiedades del proyecto** .  
  
#### <a name="to-create-a-new-data-mining-project-by-importing-an-existing-data-mining-project"></a>Para crear un nuevo proyecto de minería de datos importando un proyecto de minería de datos existente  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], en el menú **Archivo** , haga clic en **Nuevo**y, a continuación, en **Proyecto**.  
  
2.  En el cuadro de diálogo **Nuevo proyecto** , en **Plantillas instaladas**, haga clic en **Business Intelligence**, haga clic en **Analysis Services**y, después, haga clic en **Importar del servidor (multidimensional y minería de datos)**.  
  
3.  En **Nombre**, escriba un nombre para el proyecto, después especifique una ubicación y un nombre de solución, y haga clic en **Aceptar**.  
  
     Se inicia el **Asistente para importar bases de datos de Analysis Services** . Haga clic en ACEPTAR en la página de bienvenida para continuar.  
  
4.  En la página **Seleccionar base de datos de origen**, en **Servidor**, especifique la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contenga la solución que desea importar.  
  
     En **Base de datos**, elija la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contenga los objetos de minería de datos que desea importar.  
  
    > [!WARNING]  
    >  No puede especificar los objetos que desea importar; al elegir una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , se importan todos los objetos multidimensionales y de minería de datos.  
  
     Haga clic en **Siguiente**.  
  
5.  La página **Finalización del asistente**muestra el progreso de la operación de importación. No puede cancelar la operación ni cambiar los objetos que se están importando. Haga clic **Finalizar** cuando haya terminado.  
  
     El nuevo proyecto se abre de modo automático mediante [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Propiedades del proyecto &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)  
  
  

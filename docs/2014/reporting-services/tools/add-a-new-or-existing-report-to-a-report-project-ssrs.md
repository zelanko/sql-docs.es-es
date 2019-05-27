---
title: Agregar un informe nuevo o existente a un proyecto de informe (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], creating
ms.assetid: 8bc0bb53-ad8a-464d-bb6a-7fea5fa62c5c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bd6b3cc87757a8d0edc9067bd2f8f0911ccef238
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66100466"
---
# <a name="add-a-new-or-existing-report-to-a-report-project-ssrs"></a>Agregar un informe nuevo o existente a un proyecto de informe (SSRS)
  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], puede agregar un nuevo informe utilizando el Asistente para informes o agregando un nuevo informe en blanco al proyecto. También puede agregar un informe existente. Después de agregar un informe, puede ver el nombre de informe en la lista que se muestra bajo la carpeta **Informes** del proyecto.  
  
> [!NOTE]  
>  Para obtener la vista previa de un informe con orígenes de datos existentes, debe tener permisos en el origen de datos del cliente de creación de informes. Para obtener más información, consulte [crear incrustado o a un origen de datos compartido &#40;SSRS&#41;](../create-an-embedded-or-shared-data-source-ssrs.md).  
  
 Después de agregar un informe, puede definir orígenes de datos, conjuntos de datos y establecer un diseño de informe. Para comenzar, vea [Crear un informe de tabla básico &#40;Tutorial de SSRS&#41;](../create-a-basic-table-report-ssrs-tutorial.md) y [Tablas &#40;Generador de informes y SSRS&#41;](../report-design/tables-report-builder-and-ssrs.md).  
  
### <a name="to-add-a-new-report-using-the-report-wizard"></a>Para agregar un nuevo informe utilizando el Asistente para informes  
  
1.  En el Explorador de soluciones, haga clic con el botón derecho en la carpeta Informes y, después, haga clic en **Agregar nuevo informe**. Se abrirá el cuadro de diálogo **Asistente para informes** .  
  
     Los pasos del asistente le guiarán a lo largo del proceso de creación de un origen de datos, creación de un conjunto de datos con una consulta, definición de grupos, especificación de un diseño, elección de un estilo que incluya color y fuente, y creación del informe. Entre estos pasos se incluyen los siguientes:  
  
    -   **Seleccionar un origen de datos.** El primer paso para crear un informe es definir un origen de datos. El Asistente para informes muestra una lista de todos los orígenes de datos compartidos del proyecto de informe y, además, una opción para crear un nuevo origen de datos.  
  
    -   **Diseñar una consulta.** El siguiente paso es diseñar una consulta. Puede escribir la cadena de consulta, compilarla mediante el Diseñador de consultas o importar una consulta de otro informe. Para obtener información acerca de Diseñador de consultas, vea [Reporting Services Query Designers](../reporting-services-query-designers.md).  
  
    -   **Elegir un tipo de informe.** El siguiente paso es seleccionar el tipo de informe que desea. Puede elegir un informe tabular o de matriz. Un informe tabular tiene un número fijo de columnas. Un informe de matriz, o tabla de referencias cruzadas, tiene un número variable de columnas en función de los resultados de la consulta. Un informe de mapa muestra datos analíticos con un fondo geográfico.  
  
    -   **Elija un estilo.** El siguiente paso es aplicar un estilo al informe mediante una plantilla de estilo. Seleccione una plantilla para aplicar estilos al informe, como fuente, color y borde. El Diseñador de informes proporciona seis plantillas de estilo: Pizarra, bosque, corporativo, negrita, Océano y genérico. También puede agregar otras plantillas de estilo.  
  
        > [!NOTE]  
        >  Puede modificar las plantillas existentes o agregar algunas nuevas editando el archivo StyleTemplates.XML situado en la \Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies\Business Intelligence Wizards\Reports\Styles\\< lang\>carpeta, donde \<lang > es el lenguaje que utilizas (por ejemplo, si está utilizando la versión de idioma inglés [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], el nombre de la carpeta será "EN"). Esta carpeta se encuentra en el equipo donde está instalado el Diseñador de informes. Hay dos copias del archivo StyleTemplates.xml. Para modificar los estilos que se aplican mediante el Asistente para informes, modifique el archivo que se encuentra en la carpeta creada para el idioma que está usando.  
  
    -   **Asignar nombre al informe.**  El paso final es asignar un nombre al informe y comprobar los campos que se incluirán en el mismo. Una vez completados todos los pasos, el Diseñador de informes crea el informe y lo agrega al proyecto del servidor de informes.  
  
### <a name="to-add-a-new-blank-report"></a>Para agregar un nuevo informe en blanco  
  
1.  En el menú **Proyecto** , haga clic en **Agregar nuevo elemento**.  
  
2.  En **Plantillas**, haga clic en **Informe**.  
  
3.  Haga clic en **Agregar**.  
  
     Se agregará un nuevo informe en blanco al proyecto y se mostrará en la superficie de diseño.  
  
### <a name="to-add-an-existing-report"></a>Para agregar un informe existente  
  
1.  Desde el **proyecto** menú, haga clic en **agregar**y, a continuación, **elemento existente**.  
  
2.  Navegue a la ubicación del archivo .rdl, selecciónelo y, a continuación, haga clic en **Agregar**.  
  
     El informe se agregará al proyecto bajo la carpeta **Informes** . Cuando cierre y vuelva a abrir el proyecto, los informes se mostrarán ordenados alfabéticamente.  
  
## <a name="see-also"></a>Vea también  
 [Tutoriales de Reporting Services &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)  
  
  

---
title: "Crear una dimensión mediante el Asistente para dimensiones | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dimensions [Analysis Services], creating
ms.assetid: d84f66ae-7551-49bf-99d0-88368ca2dd0e
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ff4a16fdc7f18eae35de5023116a11179fb11c5b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-dimension-using-the-dimension-wizard"></a>Crear una dimensión usando el Asistente para dimensiones
  Crear una nueva dimensión usando el Asistente para dimensiones de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
### <a name="to-create-a-new-dimension"></a>Para crear una nueva dimensión  
  
1.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Dimensiones**y, después, haga clic en **Nueva dimensión**.  
  
2.  En la página **Seleccionar método de creación** del Asistente para dimensiones, seleccione **Usar una tabla existente**y, a continuación, haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  Podría tener de vez en cuando que crear una dimensión sin utilizar una tabla existente. Para más información, vea [Crear una dimensión generando una tabla que no sea de tiempos en el origen de datos](../../analysis-services/multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md) y [Crear una dimensión de tiempo generando una tabla de tiempos](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md).  
  
3.  En la página **Especificar información de origen** , siga estos procedimientos:  
  
    1.  En la lista **Vista del origen de datos** , seleccione una vista del origen de datos.  
  
    2.  En la lista **Tabla principal** , seleccione la tabla de dimensiones principal.  
  
    3.  En la lista **Columnas de clave** , revise las columnas de clave que ha seleccionado automáticamente el asistente en función de la clave principal definida en la tabla de dimensiones principal. Para cambiar esta configuración predeterminada, especifique las columnas de clave que vinculan la tabla de dimensiones a la tabla de hechos.  
  
    4.  En la lista desplegable **Columna de nombre** , revise la columna de nombre que ha seleccionado automáticamente el asistente.  
  
         Este nombre predeterminado es adecuado cuando la columna contiene información descriptiva. Sin embargo, podría desear especificar un nombre que contenga valores más significativos para el usuario final. Por ejemplo, si un atributo de categoría de producto de una dimensión Products utiliza la columna **ProductCategoryKey** como su columna de clave, puede especificar la columna **ProductCategoryName** como su columna de nombre.  
  
         Si la lista **Columnas de clave** contiene varias columnas de clave, debe especificar una columna de nombre que proporcione los valores de miembro al atributo clave. Para ello, puede crear un cálculo con nombre en la vista de origen de datos y utilizarlo como columna de nombre.  
  
    5.  Haga clic en **Siguiente**.  
  
4.  En la página **Seleccionar tablas relacionadas** , seleccione las tablas relacionadas que desea incluir en su dimensión y, a continuación, haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  La página **Seleccionar tablas relacionadas** aparece si la tabla de dimensiones principal que ha especificado tiene relaciones con otras tablas de dimensiones.  
  
5.  En la página **Seleccionar los atributos de la dimensión** , seleccione los atributos que quiera incluir en la dimensión y, a continuación, haga clic en **Siguiente**.  
  
     Opcionalmente, puede cambiar los nombres de los atributos, habilitar o deshabilitar la exploración y especificar el tipo de atributo.  
  
    > [!NOTE]  
    >  Para activar los campos **Habilitar exploración** y **Tipo de atributo** de un atributo, el atributo tiene que estar seleccionado para incluirlo en la dimensión.  
  
6.  En la columna **Tipos de cuenta integrados** de la página **Definir la inteligencia de cuentas** , seleccione el tipo de cuenta y, después, haga clic en **Siguiente**.  
  
     El tipo de cuenta debe corresponder al tipo de cuenta de la tabla de origen que aparece en la columna **Tipos de cuenta de tabla de origen** .  
  
    > [!NOTE]  
    >  La página **Definir la inteligencia de cuentas** aparece si ha definido un atributo de dimensión **Tipo de cuenta** en la página **Seleccionar los atributos de la dimensión del asistente** .  
  
7.  En la página **Finalización del asistente** , escriba un nombre para la nueva dimensión y revise la estructura de la dimensión. Si desea realizar modificaciones, haga clic **Atrás**; de lo contrario, haga clic en **Finalizar**.  
  
    > [!NOTE]  
    >  Puede utilizar el Diseñador de dimensiones una vez finalizado el Asistente para dimensiones para agregar, quitar o configurar atributos y jerarquías de la dimensión.  
  
## <a name="see-also"></a>Vea también  
 [Crear una dimensión usando una tabla existente](../../analysis-services/multidimensional-models/create-a-dimension-by-using-an-existing-table.md)  
  
  


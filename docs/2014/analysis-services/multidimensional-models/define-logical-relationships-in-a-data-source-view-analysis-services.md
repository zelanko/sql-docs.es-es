---
title: Definir relaciones lógicas en una vista del origen de datos (Analysis Services) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- adding relationships
- relationships [Analysis Services], data source views
- data source views [Analysis Services], relationships
ms.assetid: a20d6dae-e769-4131-8a59-7ef56f174220
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6ce3e78493e9e8e3f24cc7a146b2ad4afb9bfebc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200828"
---
# <a name="define-logical-relationships-in-a-data-source-view-analysis-services"></a>Definir relaciones lógicas en una vista del origen de datos (Analysis Services)
  El Asistente para vistas del origen de datos y el Diseñador de vistas del origen de datos definen automáticamente las relaciones entre las tablas agregadas a una vista del origen de datos (DSV), en función de las relaciones de la base de datos subyacente o de los criterios de coincidencia de nombres que se especifiquen.  
  
 En caso de que esté trabajando con datos de varios orígenes de datos, puede que necesite definir manualmente relaciones lógicas en la DSV para complementar las relaciones definidas automáticamente. Las relaciones son necesarias en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para identificar las tablas de hechos y dimensiones, para construir consultas para la recuperación de datos y metadatos de orígenes de datos subyacentes, y para usar las características avanzadas de Business Intelligence.  
  
 En el Diseñador de vistas del origen de datos puede definir los siguientes tipos de relaciones:  
  
-   Una relación de una tabla con otra en el mismo origen de datos.  
  
-   Una relación de una tabla consigo misma, como en una relación de elementos primarios y secundarios.  
  
-   Una relación de una tabla de un origen de datos con otra tabla de un origen de datos diferente.  
  
> [!NOTE]  
>  Las relaciones definidas en una DSV son lógicas y es posible que no reflejen las relaciones reales definidas en el origen de datos subyacente. Puede crear relaciones en el Diseñador de vistas del origen de datos que no existan en el origen de datos subyacente, y quitar las relaciones creadas por el Diseñador de vistas del origen de datos a partir de relaciones de clave externa existentes en el origen de datos subyacente.  
  
 Las relaciones incluyen una dirección. A cada valor de la columna de origen le corresponde un valor de la columna de destino. En un diagrama de la vista del origen de datos, como el diagrama que aparece en el panel **Diagrama** , una flecha sobre la línea entre dos tablas indica la dirección de la relación.  
  
 En este tema se incluyen las secciones siguientes:  
  
 [Para agregar una relación entre tablas, consultas con nombre o vistas](#bkmk_addRel)  
  
 [Para ver o modificar una relación en el panel Diagrama](#bkmk_diagrampane)  
  
 [Para ver o modificar una relación en el panel Tablas](#bkmk_tablespane)  
  
##  <a name="bkmk_addRel"></a> Para agregar una relación entre tablas, consultas con nombre o vistas  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto o conéctese a la base de datos que contiene la vista del origen de datos en que desea agregar una relación lógica.  
  
2.  En el Explorador de soluciones, expanda la carpeta **Vistas del origen de datos** y, después, haga doble clic en la vista del origen de datos para abrirla en el **Diseñador de vistas del origen de datos**.  
  
3.  Haga clic con el botón derecho en la tabla, vista o consulta con nombre a la que quiere agregar la relación en el panel **Tablas** y, después, haga clic en **Nueva relación**.  
  
    > [!NOTE]  
    >  Para buscar una tabla, vista o consulta con nombre, puede usar la opción **Buscar tabla** haciendo clic en el menú **Vista del origen de datos** o haciendo clic con el botón derecho en un área abierta de los paneles **Tablas** o **Diagrama** .  
  
4.  En el cuadro de diálogo **Especificar relación** , haga lo siguiente:  
  
    1.  Seleccione la tabla, vista o consulta con nombre adecuada en la lista **Tabla de origen (de clave externa)** .  
  
    2.  Seleccione la tabla, vista o consulta con nombre adecuada en la lista **Tabla de destino (de clave principal)** .  
  
    3.  Seleccione columnas en las listas **Columnas de origen** y **Columnas de destino** para crear una relación entre las dos tablas.  
  
         Si, al hacer un muestreo de los datos de la tabla, vista o consulta con nombre subyacente, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] detecta que ha definido la relación en la dirección equivocada (de la clave principal a la clave externa en lugar de la clave externa a la principal), se le solicitará que invierta el orden. Para invertir el orden rápidamente, haga clic en **Invertir**.  
  
         Si [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] detecta que ya existe una relación para las columnas que ha seleccionado, se le indicará. No se pueden definir relaciones duplicadas.  
  
    4.  Si lo desea, en el cuadro **Descripción** , escriba una descripción de la relación.  
  
##  <a name="bkmk_diagrampane"></a> Para ver o modificar una relación en el panel Diagrama  
  
-   En el panel **Diagrama** del **Diseñador de vistas del origen de datos**, haga clic con el botón derecho en la relación que quiere ver y haga clic en **Editar relación** (o simplemente haga doble clic en la flecha de la relación).  Use el cuadro de diálogo **Editar relación** para modificar la relación.  
  
##  <a name="bkmk_tablespane"></a> Para ver o modificar una relación en el panel Tablas  
  
1.  En el panel **Tablas** del **Diseñador de vistas del origen de datos**, busque y expanda la tabla, vista o consulta con nombre que contiene la relación que desea ver o modificar.  
  
2.  Expanda la carpeta **Relaciones** .  Las relaciones entre la tabla, vista o consulta con nombre seleccionada y las demás tablas, vistas y consultas con nombre se muestran con la columna de relaciones enumerada.  
  
3.  Haga clic con el botón derecho en la relación que quiere modificar y, después, haga clic en **Editar relación**.  
  
## <a name="see-also"></a>Vea también  
 [Vistas del origen de datos en modelos multidimensionales](data-source-views-in-multidimensional-models.md)  
  
  
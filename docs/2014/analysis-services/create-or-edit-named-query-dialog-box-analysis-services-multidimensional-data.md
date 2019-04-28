---
title: Crear o editar el cuadro de diálogo de consulta con nombre (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.createnamedquery.f1
helpviewer_keywords:
- Create Named Query dialog box
ms.assetid: 8e192ad6-a0b1-4e21-bb3f-087c93e62941
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0cc03192d0deae00b9ace6f70e72ced4883d26b1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62679773"
---
# <a name="create-or-edit-named-query-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Crear o Editar consulta con nombre (Analysis Services - Datos multidimensionales)
  Use el cuadro de diálogo **Crear/Editar consulta con nombre** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para crear o editar una consulta con nombre en el **Diseñador de vistas del origen de datos**. Una consulta con nombre puede tratarse como una tabla en la que se pueden basar otros objetos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Puede mostrar el cuadro de diálogo **Crear/Editar consulta con nombre** de distintas maneras:  
  
-   Hacer clic en **Nueva consulta con nombre** en el panel **Barra de herramientas** del **Diseñador de vistas del origen de datos**.  
  
-   Hacer clic con el botón derecho en el panel **Diagrama** del **Diseñador de vistas del origen de datos** y seleccionar **Nueva consulta con nombre**.  
  
-   Hacer clic con el botón derecho en el nombre de una consulta con nombre en el panel **Diagrama** o **Tablas** del **Diseñador de vistas del origen de datos** y seleccionar **Editar consulta con nombre**.  
  
 La consulta proporcionada debe ser un comando de consulta válido para el proveedor subyacente. La consulta se prepara para la validación con el proveedor correspondiente, así como para identificar las columnas devueltas. El cuadro de diálogo puede presentar dos vistas:  
  
-   Generador de consultas de Visual Database Tools (VDT)  
  
     El Generador de consultas de VDT proporciona a todos los usuarios un conjunto de herramientas de interfaz de usuario para crear y probar de forma visual consultas SQL.  
  
-   Generador de consultas genérico  
  
     El Generador de consultas genérico proporciona a los usuarios avanzados una interfaz de usuario más sencilla y más directa para crear y probar consultas SQL.  
  
## <a name="options"></a>Opciones  
 **Name**  
 Escriba el nombre de la consulta.  
  
 **Descripción**  
 Opcionalmente, escriba una descripción de la consulta.  
  
 **Origen de datos**  
 Especifique el origen de datos para la consulta.  
  
 **Definición de consulta**  
 La definición de la consulta proporciona una barra de herramientas y paneles (que dependerán de la vista seleccionada) para definir y probar consultas.  
  
 **Barra de herramientas**  
 Use la barra de herramientas para administrar conjuntos de datos, seleccionar los paneles que desea mostrar y controlar diversas funciones de consulta.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Cambiar a generador de consultas genérico**|Seleccione esta opción si desea mostrar únicamente las opciones disponibles para la vista del Generador de consultas genérico. Se mostrará solo una de las opciones siguientes:<br />**Panel SQL**<br />**Panel de resultados**<br />**Barra de herramientas**, que contiene únicamente **Cambiar a Generador de consultas de VDT** y **Ejecutar**<br /><br /> <br /><br /> Nota: Esta opción aparece sólo si **cambiar a generador de consultas de VDT** está seleccionada.|  
|**Cambiar a generador de consultas de VDT**|Seleccione esta opción si desea mostrar todas las opciones disponibles para la vista del Generador de consultas de Visual Database Tools (VDT).<br /><br /> Nota: Esta opción aparece sólo si **cambiar a generador de consultas genérico** está seleccionada.|  
|**Mostrar u ocultar panel de diagrama**|Muestra u oculta el **panel Diagrama**.<br /><br /> **Nota** Esta opción solo se muestra si se selecciona **Cambiar a Generador de consultas de VDT** .|  
|**Mostrar u ocultar panel de cuadrícula**|Muestra u oculta el **panel Cuadrícula**.<br /><br /> Nota: Esta opción aparece sólo si **cambiar a generador de consultas de VDT** está seleccionada.|  
|**Mostrar u ocultar panel de SQL**|Muestra u oculta el **panel de SQL**.<br /><br /> Nota: Esta opción aparece sólo si **cambiar a generador de consultas de VDT** está seleccionada.|  
|**Mostrar u ocultar panel de resultados**|Muestra u oculta el **panel Resultado**.<br /><br /> Nota: Esta opción aparece sólo si **cambiar a generador de consultas de VDT** está seleccionada.|  
|**Ejecutar**|Ejecuta la consulta. Los resultados se muestran en el **panel Resultado**.|  
|**Comprobar SQL**|Comprueba la instrucción SQL de la consulta.<br /><br /> Nota: Esta opción aparece sólo si **cambiar a generador de consultas de VDT** está seleccionada.|  
|**Orden ascendente**|Ordena de forma ascendente las filas de salida de la columna seleccionada en el **panel Cuadrícula**.<br /><br /> Nota: Esta opción aparece sólo si **cambiar a generador de consultas de VDT** está seleccionada.|  
|**Orden descendente**|Ordena de forma descendente las filas de salida de la columna seleccionada en el **panel Cuadrícula**.<br /><br /> Nota: Esta opción aparece sólo si **cambiar a generador de consultas de VDT** está seleccionada.|  
|**Quitar filtro**|Quita los criterios de ordenación, si corresponde, para la fila seleccionada en el **panel Cuadrícula**.<br /><br /> Nota: Esta opción aparece sólo si **cambiar a generador de consultas de VDT** está seleccionada.|  
|**Usar GROUP BY**|Agrega la funcionalidad de agrupamiento a la consulta.<br /><br /> Nota: Esta opción aparece sólo si **cambiar a generador de consultas de VDT** está seleccionada.|  
|**Agregar tabla**|Muestra el cuadro de diálogo **Agregar tabla** para agregar una nueva tabla o vista a la consulta. Para obtener más información sobre el cuadro de diálogo **Agregar tabla**, vea [Cuadro de diálogo Agregar tabla &#40;Analysis Services - Datos multidimensionales&#41;](add-table-dialog-box-analysis-services-multidimensional-data.md).<br /><br /> Nota: Esta opción aparece sólo si **cambiar a generador de consultas de VDT** está seleccionada.|  
  
 **Panel Diagrama**  
 Muestra en un diagrama los objetos a los que se hace referencia en la consulta. El diagrama muestra las tablas incluidas en la consulta y cómo se combinan. Active o desactive la casilla situada junto a una columna de la tabla para agregarla a (o quitarla de) la salida de la consulta.  
  
 Al agregar tablas a la consulta, el cuadro de diálogo crea combinaciones entre las tablas teniendo en cuenta las claves. Para agregar una combinación, arrastre un campo de una de las tablas a un campo de otra tabla. Para administrar una combinación, haga clic en ella con el botón secundario.  
  
 Haga clic con el botón derecho en el **panel Diagrama** para agregar o quitar tablas, seleccionar todas las tablas y mostrar u ocultar paneles.  
  
> [!NOTE]  
>  Los contenidos del **panel Diagrama**, el **panel Cuadrícula**y el **panel de SQL** están sincronizados de forma que los cambios realizados en un panel se reflejen en los otros dos paneles.  
  
> [!IMPORTANT]  
>  No es posible cambiar los tipos de consulta en el cuadro de diálogo.  
  
 **Panel de cuadrícula**  
 Muestra en una cuadrícula los objetos a los que se hace referencia en la consulta. Puede usar este panel para agregar y quitar columnas en la consulta, y para cambiar la configuración de cada columna.  
  
> [!NOTE]  
>  Los contenidos del **panel Diagrama**, el **panel Cuadrícula**y el **panel de SQL** están sincronizados de forma que los cambios realizados en un panel se reflejen en los otros dos paneles.  
  
 **Panel SQL**  
 Muestra la consulta como una instrucción SQL. Le permite modificar la instrucción SQL de la consulta.  
  
> [!NOTE]  
>  Los contenidos del **panel Diagrama**, el **panel Cuadrícula**y el **panel de SQL** están sincronizados de forma que los cambios realizados en un panel se reflejen en los otros dos paneles.  
  
 **Panel de resultados**  
 Muestra los resultados de la consulta al hacer clic en **Ejecutar** en el panel **Barra de herramientas** .  
  
## <a name="see-also"></a>Vea también  
 [Diseñadores y cuadros de diálogo de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Definir consultas con nombre en una vista del origen de datos &#40;Analysis Services&#41;](multidimensional-models/define-named-queries-in-a-data-source-view-analysis-services.md)  
  
  

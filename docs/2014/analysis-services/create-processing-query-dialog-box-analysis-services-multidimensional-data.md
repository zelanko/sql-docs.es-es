---
title: Crear el cuadro de diálogo de consulta (Analysis Services - datos multidimensionales) procesamiento | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.createprocessingquerydialog.f1
ms.assetid: c133d624-f35e-486e-be9f-ceafd906f168
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b162480fef7894a04d2488058a1e21b5bc40b602
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48077745"
---
# <a name="create-processing-query-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Crear consulta de procesamiento (Analysis Services - Datos multidimensionales)
  Use el cuadro de diálogo **Crear consulta de procesamiento** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para crear una consulta de procesamiento en la pestaña **Notificaciones** del cuadro de diálogo **Opciones de almacenamiento** . Una consulta de procesamiento es aquella que devuelve un conjunto de filas que contiene los cambios realizados en una tabla asociada a un objeto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] desde la última vez que se sondeó la tabla, con el fin de actualizar incrementalmente la caché OLAP multidimensional (MOLAP) del objeto. Analysis Services utiliza otra consulta, denominada consulta de sondeo, para sondear una tabla asociada a un objeto y determinar si ésta ha cambiado. Las consultas de procesamiento no son necesarias para actualizar completamente la caché MOLAP del objeto.  
  
 Por lo general, la consulta de procesamiento utiliza parámetros y actualmente se admiten dos parámetros:  
  
-   El valor singleton devuelto por la consulta de sondeo durante el sondeo programado anterior.  
  
-   El valor singleton devuelto por la consulta de sondeo durante el sondeo programado actual.  
  
 Por ejemplo, las consultas que se muestran en la siguiente tabla podrían utilizarse para actualizar incrementalmente la dimensión Customer en el proyecto de ejemplo Adventure Works DW de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
|Tipo de consulta|Instrucción de consulta|  
|----------------|---------------------|  
|Consulta de sondeo|`SELECT`<br /><br /> `MAX([CustomerKey]) AS LastCustomerKey`<br /><br /> `FROM`<br /><br /> `[dbo].[DimCustomer]`|  
|Consulta de procesamiento|`SELECT`<br /><br /> `*`<br /><br /> `FROM`<br /><br /> `[dbo].[DimCustomer]`<br /><br /> `WHERE`<br /><br /> `(CustomerKey > COALESCE (@Param1, - 1))`<br /><br /> `AND (CustomerKey <= @Param2)`|  
  
 Para obtener más información sobre las actualizaciones incrementales para notificaciones de sondeos programados, vea [Almacenamiento en caché automático &#40;Particiones&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
 Para mostrar el cuadro de diálogo **Crear consulta de procesamiento** , haga clic en **...** en la columna **Consulta de procesamiento** de la cuadrícula de la opción **Sondeo programado** en la pestaña **Notificaciones** del cuadro de diálogo **Opciones de almacenamiento** . Para obtener más información sobre la pestaña **Notificaciones** del cuadro de diálogo **Opciones de almacenamiento**, vea [Notificaciones &#40;cuadro de diálogo Opciones de almacenamiento&#41; &#40;Analysis Services - Datos multidimensionales&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md).  
  
 La consulta proporcionada debe ser un comando de consulta válido para el proveedor subyacente. La consulta se prepara para la validación con el proveedor correspondiente, así como para identificar las columnas devueltas. El cuadro de diálogo puede presentar dos vistas:  
  
-   Generador de consultas de Visual Database Tools (VDT)  
  
     El Generador de consultas de VDT proporciona a todos los usuarios un conjunto de herramientas de interfaz de usuario para crear y probar de forma visual consultas SQL.  
  
-   Generador de consultas genérico  
  
     El Generador de consultas genérico proporciona a los usuarios avanzados una interfaz de usuario más sencilla y más directa para crear y probar consultas SQL.  
  
## <a name="options"></a>Opciones  
 **Origen de datos**  
 Especifique el origen de datos para la consulta.  
  
 **Definición de consulta**  
 La definición de la consulta proporciona una barra de herramientas y paneles (que dependerán de la vista seleccionada) para definir y probar consultas.  
  
 **Barra de herramientas**  
 Use la barra de herramientas para administrar conjuntos de datos, seleccionar los paneles que desea mostrar y controlar diversas funciones de consulta.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Cambiar a generador de consultas genérico**|Seleccione esta opción si desea mostrar únicamente las opciones disponibles para la vista del Generador de consultas genérico. Se mostrará solo una de las opciones siguientes:<br /><br /> **Panel SQL**<br /><br /> **Panel de resultados**<br /><br /> **Barra de herramientas**, que contiene únicamente **Cambiar a Generador de consultas de VDT** y **Ejecutar**<br /><br /> Nota: Esta opción solo se muestra si se selecciona **Cambiar a Generador de consultas de VDT** .|  
|**Cambiar a generador de consultas de VDT**|Seleccione esta opción si desea mostrar todas las opciones disponibles para la vista del Generador de consultas de Visual Database Tools (VDT).<br /><br /> Nota: Esta opción solo se muestra si se selecciona **Cambiar a Generador de consultas genérico** .|  
|**Mostrar u ocultar panel de diagrama**|Muestra u oculta el **panel Diagrama**.<br /><br /> **Nota** Esta opción solo se muestra si se selecciona **Cambiar a Generador de consultas de VDT** .|  
|**Mostrar u ocultar panel de cuadrícula**|Muestra u oculta el **panel Cuadrícula**.<br /><br /> Nota: Esta opción solo se muestra si se selecciona **Cambiar a Generador de consultas de VDT** .|  
|**Mostrar u ocultar panel de SQL**|Muestra u oculta el **panel de SQL**.<br /><br /> Nota: Esta opción solo se muestra si se selecciona **Cambiar a Generador de consultas de VDT** .|  
|**Mostrar u ocultar panel de resultados**|Muestra u oculta el **panel Resultado**.<br /><br /> Nota: Esta opción solo se muestra si se selecciona **Cambiar a Generador de consultas de VDT** .|  
|**Ejecutar**|Ejecuta la consulta. Los resultados se muestran en el **panel Resultado**.|  
|**Comprobar SQL**|Comprueba la instrucción SQL de la consulta.<br /><br /> Nota: Esta opción solo se muestra si se selecciona **Cambiar a Generador de consultas de VDT** .|  
|**Orden ascendente**|Ordena de forma ascendente las filas de salida de la columna seleccionada en el **panel Cuadrícula**.<br /><br /> Nota: Esta opción solo se muestra si se selecciona **Cambiar a Generador de consultas de VDT** .|  
|**Orden descendente**|Ordena de forma descendente las filas de salida de la columna seleccionada en el **panel Cuadrícula**.<br /><br /> Nota: Esta opción solo se muestra si se selecciona **Cambiar a Generador de consultas de VDT** .|  
|**Quitar filtro**|Quita los criterios de ordenación, si corresponde, para la fila seleccionada en el **panel Cuadrícula**.<br /><br /> Nota: Esta opción solo se muestra si se selecciona **Cambiar a Generador de consultas de VDT** .|  
|**Usar GROUP BY**|Agrega la funcionalidad de agrupamiento a la consulta.<br /><br /> Nota: Esta opción solo se muestra si se selecciona **Cambiar a Generador de consultas de VDT** .|  
|**Agregar tabla**|Muestra el cuadro de diálogo **Agregar tabla** para agregar una nueva tabla o vista a la consulta. Para obtener más información sobre el cuadro de diálogo **Agregar tabla**, vea [Cuadro de diálogo Agregar tabla &#40;Analysis Services - Datos multidimensionales&#41;](add-table-dialog-box-analysis-services-multidimensional-data.md).<br /><br /> Nota: Esta opción solo se muestra si se selecciona **Cambiar a Generador de consultas de VDT** .|  
  
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
  
  

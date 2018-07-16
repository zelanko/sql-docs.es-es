---
title: Crear el cuadro de diálogo (Analysis Services - datos multidimensionales) de consulta de sondeo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.createpollingquerydialog.f1
ms.assetid: 0f2902b5-796a-4eb0-be03-01514dc01b9a
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f1c7ca8d5c2594668283887c23f7d976a1fc3359
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37236235"
---
# <a name="create-polling-query-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Crear consulta de sondeo (Analysis Services - Datos multidimensionales)
  Utilice el cuadro de diálogo **Crear consulta de sondeo** en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para crear una consulta de sondeo en la pestaña **Notificaciones** del cuadro de diálogo **Opciones de almacenamiento** . Una consulta de sondeo es, por lo general, una consulta singleton que devuelve un valor que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] puede utilizar para determinar si los cambios se realizaron en una tabla o en otro objeto relacional. Para mostrar el cuadro de diálogo **Crear consulta de sondeo**, haga clic en el botón de puntos suspensivos (**…**) que se encuentra en la columna **Consulta de sondeo** de la cuadrícula correspondiente a la opción **Sondeo programado**, en la pestaña **Notificaciones** del cuadro de diálogo **Opciones de almacenamiento**. Para más información sobre la pestaña **Notificaciones** del cuadro de diálogo **Opciones de almacenamiento**, vea [Notificaciones &#40;cuadro de diálogo Opciones de almacenamiento&#41; &#40;Analysis Services - Datos multidimensionales&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md).  
  
 El tipo de valor que debe devolver la consulta de sondeo depende del tipo de actualización planeado para la caché de OLAP multidimensional (MOLAP) del objeto, en función de la tabla que se está consultando:  
  
-   Si no se ha seleccionado **Habilitar actualizaciones incrementales** en la pestaña **Notificaciones** del cuadro de diálogo **Opciones de almacenamiento** , [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] actualiza completamente la caché de MOLAP correspondiente al objeto si se detecta un cambio durante el sondeo programado. La consulta de sondeo utilizada debe determinar si se han agregado registros a la tabla desde el último período de sondeo.  
  
-   Si se ha seleccionado **Habilitar actualizaciones incrementales** en la pestaña **Notificaciones** del cuadro de diálogo **Opciones de almacenamiento** , [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] actualiza incrementalmente la caché de MOLAP correspondiente al objeto cuando se detecta un cambio durante el sondeo programado. La consulta de sondeo usada debe determinar el último registro de la tabla.  
  
 Por ejemplo, puede utilizar las siguientes consultas de sondeo para proporcionar actualizaciones completas o incrementales para la dimensión Cliente en la base de datos de ejemplo [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
|Tipo de actualización|Consulta de sondeo|  
|-----------------|-------------------|  
|Actualización completa|`SELECT`<br /><br /> `COUNT(*) AS TotalCount`<br /><br /> `FROM`<br /><br /> `[dbo].[DimCustomer]`|  
|Actualización incremental|`SELECT`<br /><br /> `MAX([CustomerKey]) AS LastCustomerKey`<br /><br /> `FROM`<br /><br /> `[dbo].[DimCustomer]`|  
  
 Para más información sobre las actualizaciones incrementales para notificaciones de sondeos programados, vea [Almacenamiento en caché automático &#40;Particiones&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
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
|**Cambiar a generador de consultas genérico**|Seleccione esta opción si desea mostrar únicamente las opciones disponibles para la vista del Generador de consultas genérico. Se mostrará solo una de las opciones siguientes:<br /><br /> **Panel SQL**<br /><br /> **Panel de resultados**<br /><br /> **Barra de herramientas**, que contiene únicamente **Cambiar a Generador de consultas de VDT** y **Ejecutar**<br /><br /> <br /><br /> Nota: Esta opción solo se muestra si se selecciona **Cambiar a Generador de consultas de VDT** .|  
|**Cambiar a generador de consultas de VDT**|Seleccione esta opción si desea mostrar todas las opciones disponibles para la vista del Generador de consultas de Visual Database Tools (VDT).<br /><br /> Nota: Esta opción solo se muestra si se selecciona **Cambiar a Generador de consultas genérico** .|  
|**Mostrar u ocultar panel de diagrama**|Muestra u oculta el **panel Diagrama**.<br /><br /> Nota: Esta opción solo se muestra si se selecciona **Cambiar a Generador de consultas de VDT** .|  
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
  
  

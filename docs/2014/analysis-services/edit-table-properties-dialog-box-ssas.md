---
title: Cuadro de diálogo Editar propiedades de tabla (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.edittablepropdb.f1
ms.assetid: 8d913e83-7246-44cc-8fc7-31729023c0d8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1fefc72d81129ac4691f35209f25c4f348272c81
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081434"
---
# <a name="edit-table-properties-dialog-box-ssas"></a>Editar propiedades de tabla, cuadro de diálogo (SSAS)
  El cuadro de diálogo **Editar propiedades de tabla** le permite ver y modificar las propiedades de las tablas importadas en el diseñador de modelos mediante el Asistente para la importación de tablas. Para obtener acceso a este cuadro de diálogo, en el diseñador de modelos, seleccione una tabla, haga clic en el menú **Tabla** y, a continuación, haga clic en **Propiedades de tabla**.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 Las opciones de este cuadro de diálogo varían dependiendo de si importó los datos originalmente seleccionando las tablas en una lista o usando una consulta SQL.  
  
## <a name="table-preview-mode"></a>Modo de vista previa de tabla  
 **Nombre de tabla**  
 Muestra el nombre de la tabla de datos en el modelo.  
  
> [!NOTE]  
>  No puede modificar el nombre aquí. Sin embargo, puede cambiar el nombre de la tabla haciendo clic con el botón secundario en la pestaña de la tabla en la parte inferior del diseñador de modelos.  
  
 **Nombre de la conexión**  
 Muestra el nombre de la conexión que se usa actualmente.  
  
 **Nombre de origen**  
 Se usa para mostrar o cambiar la tabla de la que se obtienen los datos.  
  
 Si se cambia el origen a una tabla que tiene columnas distintas que la tabla actual, aparece un mensaje que advierte que las columnas son distintas. En ese caso, debe seleccionar las columnas que desea poner en la tabla actual y hacer clic en **Guardar**. Puede reemplazar toda la tabla activando la casilla de la izquierda de la tabla.  
  
> [!NOTE]  
>  Al cambiar el origen de datos de una tabla, lo que se hace es reemplazar el contenido de la tabla actual con el contenido de la nueva tabla de origen.  
  
 **Nombres de columna de**  
 |||  
|-|-|  
|**Origen**|Seleccione esta opción para reemplazar los nombres de columna actuales por los nombres de columna de la tabla de origen seleccionada.|  
|**Modela**|Seleccione esta opción para usar los nombres de columna actual tal como aparecen en el modelo.|  
  
 **Actualizar vista previa**  
 Haga clic en esta opción para ver las columnas de datos de la tabla de origen actualmente seleccionada.  
  
 **Cambiar a**  
 |||  
|-|-|  
|**Vista previa de tabla**|Seleccione esta opción de la lista para obtener una vista previa de la tabla seleccionada y un número limitado de filas de datos.|  
|**Editor de consultas**|Seleccione esta opción para ver la consulta en el origen de datos seleccionado. Esta opción no está disponible para todos los orígenes de datos.|  
  
 **Casilla en el encabezado de columna**  
 Active la casilla para incluir la columna en la importación de datos. Desactive la casilla para quitar la columna de la importación de datos.  
  
 **Botón de flecha abajo en el encabezado de columna**  
 Filtre los datos de la columna.  
  
 **Borrar filtros de fila**  
 Haga clic en esta opción para quitar los filtros que se hayan aplicado.  
  
 **Aceptar**  
 Haga clic en esta opción para aplicar todos los cambios, incluso el reemplazo de columnas.  
  
## <a name="query-design-mode"></a>Modo de diseño de consulta  
 **Nombre de tabla**  
 Muestra el nombre de la tabla de datos en el modelo.  
  
> [!NOTE]  
>  Aquí no se puede modificar el nombre. El nombre de la tabla se puede cambiar haciendo clic con el botón secundario en la pestaña de la tabla de la parte inferior del diseñador.  
  
 **Nombre de la conexión**  
 Muestra el nombre de la conexión que se usa actualmente.  
  
 **Cambiar a**  
 |||  
|-|-|  
|**Vista previa de tabla**|Seleccione esta opción para obtener una vista previa de la tabla seleccionada y algunas filas de datos.|  
|**Editor de consultas**|Seleccione esta opción para ver la consulta que se emitirá para el origen de datos seleccionado.|  
  
 **Instrucción SQL**  
 Muestra la instrucción SQL que se emite al origen de datos actual para recuperar filas. De forma predeterminada, se recuperan todas las filas, pero se puede recuperar un subconjunto de filas diseñando un filtro o editando la instrucción SQL manualmente.  
  
 **Vali**  
 Haga clic en esta opción para comprobar si la instrucción es sintácticamente correcta para el origen de datos y el proveedor seleccionados.  
  
 **Diseño**  
 Haga clic en esta opción para abrir un diseñador de consultas visual y generar una instrucción de consulta. Para obtener información acerca de cómo utilizar el diseñador, presione F1 desde el diseñador.  
  
 **Aceptar**  
 Haga clic en esta opción para aplicar todos los cambios, incluso el reemplazo de columnas.  
  
## <a name="see-also"></a>Consulte también  
 [Definir tablas y columnas &#40;SSAS tabular&#41;](tabular-models/tables-and-columns-ssas-tabular.md)  
  
  

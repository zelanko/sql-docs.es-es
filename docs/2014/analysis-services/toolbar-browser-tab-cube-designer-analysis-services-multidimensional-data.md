---
title: Barra de herramientas (pestaña explorador, diseñador de cubos) (Analysis Services-datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a1c6272d-e514-456b-9995-b73fec0112a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fe356d15c0602f33ec9c59ee463a69783686899b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66066146"
---
# <a name="toolbar-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>Barra de herramientas (pestaña Explorador, Diseñador de cubos) (Analysis Services - Datos multidimensionales)
  Utilice las características de la **Barra de herramientas** del Diseñador de cubos para realizar operaciones comunes al diseñar o examinar un cubo o su objeto, o al crear una consulta MDX. Entre las operaciones comunes en tiempo de diseño y a la vista de consulta se halla la configuración del contexto de usuario, el procesamiento de objetos y la configuración del idioma predeterminado.  
  
 En la tabla siguiente se describen los botones de la **Barra de herramientas** y sus funciones.  
  
|Botón|Descripción|  
|------------|-----------------|  
|**Editar como texto**|No está habilitado para este tipo de origen de datos.|  
|**Importar**|Importa una consulta existente desde un archivo de definición de informe (.rdl) del sistema de archivos.|  
|![Cambiar a la vista de la consulta MDX](media/rsqdicon-commandtypemdx.gif "Cambiar a la vista de la consulta MDX")|Cambia al tipo de comando MDX.|  
|![Actualizar datos de resultados](media/rsqdicon-refresh.gif "Actualizar datos de resultados")|Actualiza los metadatos desde el origen de datos.|  
|![Agregar miembro calculado](media/rsqdicon-addcalculatedmember.gif "Agregar miembro calculado")|Muestra el cuadro de diálogo **Generador de miembros calculados** .|  
|![Alternar para mostrar celdas vacías](media/rsqdicon-showemptycells.gif "Alternar para mostrar celdas vacías")|Muestra y oculta las celdas vacías del panel Datos. Esto equivale a utilizar la cláusula NON EMPTY en MDX.|  
|![Ejecutar la consulta automáticamente](media/rsqdicon-autoexecute.gif "Ejecutar la consulta automáticamente")|Ejecuta automáticamente la consulta y muestra el resultado cada vez que se realiza un cambio. Los resultados se mostrarán en el panel Datos.|  
|![Botón Mostrar agregaciones](media/rsqdicon-showaggregations.gif "Botón Mostrar agregaciones")|Muestra agregaciones en el panel Datos.|  
|![Eliminar](media/rsqdicon-delete.gif "Eliminar")|Elimina la columna seleccionada en el panel Datos de la consulta.|  
|![Icono del cuadro de diálogo Parámetros de consulta](media/iconqueryparameter.gif "Icono del cuadro de diálogo Parámetros de consulta")|Muestra el cuadro de diálogo **Parámetros de consulta** . Al especificar valores para un parámetro de consulta, se crea automáticamente un parámetro con el mismo nombre.|  
|![Botón Preparar consulta](media/rsqdicon-preparequery.gif "Botón Preparar consulta")|Prepara la consulta.|  
|![Ejecutar la consulta](media/rsqdicon-run.gif "Ejecutar la consulta")|Ejecuta la consulta y muestra los resultados en el panel Datos.|  
|![Cancelar la consulta](media/rsqdicon-cancel.gif "Cancelar la consulta")|Cancela la consulta.|  
|![Cambiar al modo de diseño](media/rsqdicon-designmode.gif "Cambiar al modo de diseño")|Alterna el modo de diseño y el modo de consulta.|  
  
 En general, los botones de la barra de herramientas son los mismos para **Modo de diseño** y **Modo de consulta**. Sin embargo, los botones siguientes no están habilitado para el Modo de consulta:  
  
-   **Editar como texto**  
  
-   **Agregar miembro calculado** (![Agregar miembro calculado](media/rsqdicon-addcalculatedmember.gif "Agregar miembro calculado"))  
  
-   **Mostrar celdas vacías** (![alternar para mostrar celdas vacías](media/rsqdicon-showemptycells.gif "Alternar para mostrar celdas vacías"))  
  
-   **Ejecución** automática (![ejecución automática de la consulta](media/rsqdicon-autoexecute.gif "Ejecutar la consulta automáticamente"))  
  
-   **Mostrar agregaciones** (![botón Mostrar agregaciones](media/rsqdicon-showaggregations.gif "Botón Mostrar agregaciones"))  
  
## <a name="options"></a>Opciones  
  
|Opción|Descripción|  
|------------|-----------------|  
|**Proceso**|Haga clic en esta opción para mostrar el cuadro de diálogo **Procesar** y procesar el cubo. Para obtener más información sobre el cuadro de diálogo **Proceso**, vea [Cuadro de diálogo Proceso &#40;Analysis Services - Datos multidimensionales&#41;](process-dialog-box-analysis-services-multidimensional-data.md).|  
|**Cambiar usuario**|Haga clic para mostrar el cuadro de diálogo **contexto de seguridad** y cambiar el usuario y el rol usados en la pestaña **Explorador** . Para obtener más información sobre el cuadro de diálogo **contexto de seguridad** , vea [cuadro de diálogo contexto de seguridad &#40;Analysis Services-&#41;de datos multidimensionales ](security-context-dialog-box-analysis-services-multidimensional-data.md).|  
|**Volver a conectar**|Haga clic para volver a conectar la pestaña **Cálculos** a la instancia y base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que contiene el cubo si se desconecta la sesión de la pestaña **Explorador** por pérdida de conexión o exceso de tiempo de espera.|  
|**Actualizar**|Haga clic para actualizar los paneles **Metadatos** e **Informes** .|  
|**Orden ascendente**|Haga clic para ordenar los elementos del mismo nivel de la fila seleccionada en el panel **Informe** en orden ascendente para el idioma especificado en **Idioma**.<br /><br /> **Nota:** Esta opción solo se habilita si se selecciona una celda en el panel **informes** .|  
|**Orden descendente**|Haga clic para ordenar los elementos del mismo nivel de la fila seleccionada en el panel **Informe** en orden descendente para el idioma especificado en **Idioma**.<br /><br /> Nota: Solo se habilitará esta opción si se selecciona una celda en el panel **Informes** .|  
|**Autofiltro**|Haga clic para filtrar automáticamente los resultados en el panel **Resultado** .|  
|**Mostrar solamente superior o inferior**|Seleccione un valor o porcentaje para mostrar solamente el número o porcentaje máximo o mínimo de celdas en el panel **Informe** según la medida seleccionada.<br /><br /> Para obtener más información sobre esta opción, vea [TopCount &#40;MDX&#41;](/sql/mdx/topcount-mdx), [TopPercent &#40;MDX&#41;](/sql/mdx/toppercent-mdx), [BottomCount &#40;MDX&#41;](/sql/mdx/bottomcount-mdx) y [BottomPercent &#40;MDX&#41;](/sql/mdx/bottompercent-mdx).|  
|**Subtotal**|Haga clic para mostrar los subtotales.|  
|**Totales de todos los elementos**|Haga clic para mostrar los totales de todos los miembros en el panel **Informe** .|  
|**Mostrar celdas vacías**|Haga clic para mostrar las celdas vacías en el panel **Informe** .|  
|**Borrar resultados**|Haga clic para borrar los resultados del panel **Informe** .|  
|**Comandos y opciones**|Haga clic para mostrar el cuadro de diálogo **Comandos y opciones** y editar las propiedades avanzadas para el control PivotTable de Microsoft Office 11.0 en el panel **Informe** . Para obtener más información acerca del cuadro de diálogo **Comandos y opciones** , vea la documentación de Microsoft Office.|  
|**Perspectiva**|Seleccione la perspectiva desde la que desea ver los datos y metadatos en los paneles **Metadatos** e **Informe** .<br /><br /> Para ver el cubo sin utilizar una perspectiva, seleccione el nombre del cubo.|  
|**Lenguaje**|Seleccione el idioma en el que desea ver los datos y metadatos de los paneles **Metadatos** e **Informe** .<br /><br /> Para ver el cubo en el idioma predeterminado, seleccione **Predeterminado**.|  
  
  

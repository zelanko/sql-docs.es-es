---
title: Diseñador de consultas MDX (SSAS) de Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.asmdxquerydes.f1
ms.assetid: a2fb0b79-802a-4dac-bd9a-32dfe2e8c4d4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 23bdc92e18a7f2cae351faddd69370c9e08a7371
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66062506"
---
# <a name="analysis-services-mdx-query-designer-ssas"></a>Diseñador de consultas MDX de Analysis Services (SSAS)
  El diseñador de consultas de expresiones multidimensionales (MDX) de Analysis Services proporciona una interfaz gráfica de usuario para ayudarle a crear consultas MDX para un origen de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. El diseñador gráfico de consultas MDX tiene dos modos: modo de diseño y modo de consulta. Cada modo proporciona un panel de metadatos desde el que puede arrastrar miembros de los cubos seleccionados para crear una consulta MDX que recupera los datos que desee usar.  
  
> [!IMPORTANT]  
>  Los usuarios tienen acceso a los orígenes de datos cuando crean y ejecutan las consultas. Debe conceder permisos mínimos para los orígenes de datos, por ejemplo permisos de solo lectura.  
>   
>  Para conectarse al origen de datos cuando se ejecuta una consulta se utilizan las credenciales del usuario actual, no las credenciales especificadas en la página Información de suplantación.  
  
 En las secciones siguientes se describen los botones de la barra de tareas y los paneles del diseñador para cada modo del diseñador gráfico de consultas.  
  
## <a name="graphical-mdx-query-designer-in-design-mode"></a>Diseñador gráfico de consultas MDX en modo de diseño  
 Al editar una consulta MDX, el diseñador gráfico de consultas MDX se abre en modo de diseño.  
  
 En la siguiente ilustración se indican los nombres de los paneles del modo de diseño.  
  
 ![Diseñador de consultas MDX de Analysis Services, vista de diseño](media/rsqd-dsawas-mdx-designmode.gif "Diseñador de consultas MDX de Analysis Services, vista de diseño")  
  
 En la tabla siguiente aparecen los paneles de este modo:  
  
|Panel|Función|  
|----------|--------------|  
|Botón Selección de cubo (**...**)|Muestra el cubo seleccionado actualmente.|  
|Panel Metadatos|Muestra una lista jerárquica de medidas, indicadores clave de rendimiento (KPI) y dimensiones definidas en el cubo seleccionado.|  
|Panel Miembros calculados|Muestra los miembros calculados definidos actualmente que se encuentran disponibles para utilizarse en la consulta.|  
|Panel Filtro|Se usa a fin de elegir dimensiones y jerarquías relacionadas para filtrar datos en el origen y limitar datos devueltos.|  
|Panel Datos|Muestra los encabezados de columna del conjunto de resultados mientras arrastra elementos de los paneles Metadatos y Miembros calculados. Actualiza automáticamente el conjunto de resultados si el botón **Ejecución automática** está seleccionado.|  
  
 Puede arrastrar dimensiones, medidas y KPI desde el panel Metadatos, y los miembros calculados desde el panel Miembros calculados al panel Datos. En el panel Filtro, puede seleccionar dimensiones y jerarquías relacionadas, y establecer expresiones de filtro para limitar los datos disponibles en la consulta. Si el botón de alternancia **Ejecución automática** (![Ejecutar la consulta automáticamente](media/rsqdicon-autoexecute.gif "Ejecutar la consulta automáticamente")) de la barra de herramientas está seleccionado, el diseñador de consultas ejecuta la consulta cada vez que coloque un objeto de metadatos en el panel Datos. Puede ejecutar la consulta manualmente con el botón **Ejecutar** (![Ejecutar la consulta](media/rsqdicon-run.gif "Ejecutar la consulta")) de la barra de herramientas.  
  
 Al crear una consulta MDX en este modo, se incluyen automáticamente en la consulta las propiedades adicionales siguientes:  
  
 **Propiedades de miembro** MEMBER_CAPTION, MEMBER_UNIQUE_NAME  
  
 **Propiedades de la celda** VALUE, BACK_COLOR, FORE_COLOR, FORMATTED_VALUE, FORMAT_STRING, FONT_NAME, FONT_SIZE, FONT_FLAGS  
  
 Si desea especificar sus propias propiedades adicionales, debe modificar manualmente la consulta MDX en el modo de consulta.  
  
 No se admite la importación de una consulta .mdx desde un archivo.  
  
> [!NOTE]  
>  Para más información sobre MDX e información general sobre el diseñador de consultas MDX, vea "Editor de consultas MDX (Analysis Services - Datos multidimensionales)" en los [Libros en pantalla de SQL Server](https://go.microsoft.com/fwlink/?linkid=98335).  
  
### <a name="graphical-mdx-query-designer-toolbar-in-design-mode"></a>Barra de herramientas del diseñador gráfico de consultas MDX en modo de diseño  
 La barra de herramientas del diseñador de consultas proporciona botones que le ayudan a diseñar consultas MDX mediante la interfaz gráfica. En la tabla siguiente se describen los botones y sus funciones.  
  
|Botón|Descripción|  
|------------|-----------------|  
|**Editar como texto**|No está habilitado para este tipo de origen de datos.|  
|**Importar**|Importa una consulta existente desde un archivo de definición de informe (.rdl) del sistema de archivos.|  
|![Cambiar a la vista de la consulta MDX](media/rsqdicon-commandtypemdx.gif "Cambiar a la vista de la consulta MDX")|Cambia al tipo de comando MDX.|  
|![Actualizar datos de resultados](media/rsqdicon-refresh.gif "Actualizar datos de resultados")|Actualiza los metadatos desde el origen de datos.|  
|![Add calculated member](media/rsqdicon-addcalculatedmember.gif "Add calculated member")|Muestra el cuadro de diálogo **Generador de miembros calculados** .|  
|![Alternar para mostrar celdas vacías](media/rsqdicon-showemptycells.gif "Alternar para mostrar celdas vacías")|Muestra y oculta las celdas vacías del panel Datos. Esto equivale a utilizar la cláusula NON EMPTY en MDX.|  
|![Ejecutar la consulta automáticamente](media/rsqdicon-autoexecute.gif "Ejecutar la consulta automáticamente")|Ejecuta automáticamente la consulta y muestra el resultado cada vez que se realiza un cambio. Los resultados se mostrarán en el panel Datos.|  
|![Botón Mostrar agregaciones](media/rsqdicon-showaggregations.gif "Botón Mostrar agregaciones")|Muestra agregaciones en el panel Datos.|  
|![Eliminar](media/rsqdicon-delete.gif "Eliminar")|Elimina la columna seleccionada en el panel Datos de la consulta.|  
|![Icono del cuadro de diálogo Parámetros de consulta](media/iconqueryparameter.gif "Icono del cuadro de diálogo Parámetros de consulta")|Muestra el cuadro de diálogo **Parámetros de consulta** . Al especificar valores para un parámetro de consulta, se crea automáticamente un parámetro con el mismo nombre.|  
|![Botón Preparar consulta](media/rsqdicon-preparequery.gif "Botón Preparar consulta")|Prepara la consulta.|  
|![Ejecutar la consulta](media/rsqdicon-run.gif "Ejecutar la consulta")|Ejecuta la consulta y muestra los resultados en el panel Datos.|  
|![Cancelar la consulta](media/rsqdicon-cancel.gif "Cancelar la consulta")|Cancela la consulta.|  
|![Cambiar al modo de diseño](media/rsqdicon-designmode.gif "Cambiar al modo de diseño")|Alterna el modo de diseño y el modo de consulta.|  
  
## <a name="graphical-mdx-query-designer-in-query-mode"></a>Diseñador gráfico de consultas MDX en modo de consulta  
 Para cambiar el diseñador gráfico de consultas al modo **Consulta** , haga clic en el botón **Modo de diseño** de la barra de herramientas.  
  
 En la ilustración siguiente se indican los nombres de los paneles del modo de consulta.  
  
 ![Diseñador de consultas MDX de Analysis Services, vista de consulta](media/rsqd-dsawas-mdx-querymode.gif "Diseñador de consultas MDX de Analysis Services, vista de consulta")  
  
 En la tabla siguiente aparecen los paneles de este modo:  
  
|Panel|Función|  
|----------|--------------|  
|Botón Selección de cubo (**...**)|Muestra el cubo seleccionado actualmente.|  
|Panel Metadatos/Funciones/Plantillas|Muestra una lista jerárquica de medidas, KPI y dimensiones definidas en el cubo seleccionado.|  
|Panel de consulta|Muestra el texto de consulta.|  
|Panel Resultado|Muestra los resultados de la ejecución de la consulta.|  
  
 El panel Metadatos muestra pestañas de **Metadatos**, **Funciones**y **Plantillas**. Desde la pestaña **Metadatos** , puede arrastrar dimensiones, jerarquías, KPI y medidas al panel Consulta MDX. Desde la pestaña **Funciones** , puede arrastrar funciones hasta el panel Consulta MDX. Desde la pestaña **Plantillas** , puede agregar plantillas MDX al panel Consulta MDX. Cuando ejecute la consulta, en el panel Resultado se mostrarán los resultados de la consulta MDX.  
  
 Puede ampliar la consulta MDX predeterminada generada en modo de diseño para que incluya propiedades de miembro y de celda adicionales. Al ejecutar la consulta, estos valores no aparecen en el conjunto de resultados. Sin embargo, se devuelven con la colección de campos de conjunto de datos, por lo que puede usar estos valores.  
  
### <a name="graphical-query-designer-toolbar-in-query-mode"></a>Barra de herramientas del diseñador gráfico de consultas en modo de consulta  
 La barra de herramientas del diseñador de consultas proporciona botones que le ayudan a diseñar consultas MDX mediante la interfaz gráfica.  
  
 Los botones de la barra de herramientas son idénticos en los modos de diseño y de consulta. Sin embargo, los siguientes botones no están habilitados para el modo de consulta:  
  
-   **Editar como texto**  
  
-   **Agregar miembro calculado** (![Add calculated member](media/rsqdicon-addcalculatedmember.gif "Add calculated member"))  
  
-   **Mostrar celdas vacías** (![Alternar para mostrar celdas vacías](media/rsqdicon-showemptycells.gif "Alternar para mostrar celdas vacías"))  
  
-   **Ejecución automática** (![Ejecutar la consulta automáticamente](media/rsqdicon-autoexecute.gif "Ejecutar la consulta automáticamente"))  
  
-   **Mostrar agregaciones** (![Botón Mostrar agregaciones](media/rsqdicon-showaggregations.gif "Botón Mostrar agregaciones"))  
  
  

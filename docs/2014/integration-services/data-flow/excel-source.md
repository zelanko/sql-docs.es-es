---
title: Origen de Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.excelsource.f1
helpviewer_keywords:
- Excel [Integration Services]
- sources [Integration Services], Excel
ms.assetid: e66349f3-b1b8-4763-89b7-7803541a4d62
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 37eb17ccaa418a6d81ef4caa461af50e505a8747
ms.sourcegitcommit: c37777216fb8b464e33cd6e2ffbedb6860971b0d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82087157"
---
# <a name="excel-source"></a>Origen de Excel
  El origen de Excel extrae datos de hojas de cálculo o de rangos de libros de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel.  
  
 El origen de Excel ofrece cuatro modos de acceso a datos distintos para extraer datos:  
  
-   Una tabla o vista.  
  
-   Una tabla o vista especificadas en una variable.  
  
-   Los resultados de una instrucción SQL. La consulta puede tener parámetros.  
  
-   Los resultados de una instrucción SQL, almacenados en una variable.  
  
> [!IMPORTANT]  
>  En Excel, una hoja o un rango equivalen a una tabla o vista. La lista de tablas disponibles en los editores de Origen y Destino de Excel muestra las hojas de cálculo existentes (identificadas con el signo $ anexado al nombre de la hoja de cálculo, como, por ejemplo, Hoja1$) y rangos con nombre (identificados por la falta del signo $, como por ejemplo, MiRango). Para obtener más información, vea la sección Consideraciones de uso.  
  
 El origen de Excel usa un Administrador de conexiones con Excel para conectar con un origen de datos y el Administrador de conexiones especifica el archivo de libro que se debe usar. Para más información, consulte [Excel Connection Manager](../connection-manager/excel-connection-manager.md).  
  
 El origen de Excel tiene una salida normal y una salida de error.  
  
## <a name="usage-considerations"></a>Consideraciones de uso  
 El Administrador de conexiones con Excel usa el Proveedor OLE DB de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para Jet 4.0 y el controlador ISAM (Método de acceso secuencial indexado) de Excel asociado para conectar con orígenes Excel de datos y leer y escribir datos en ellos.  
  
 Muchos artículos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base documentan el comportamiento de este proveedor y el controlador. Aunque estos artículos no son específicos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ni de Servicios de transformación de datos (su predecesor), posiblemente le interese conocer determinados comportamientos que pueden provocar resultados inesperados. Para obtener información general sobre el uso y el comportamiento del controlador de Excel, vea [Cómo usar ADO con datos de Excel procedentes de Visual Basic o VBA](https://support.microsoft.com/kb/257819).  
  
 Los siguientes comportamientos del proveedor Jet con el controlador de Excel pueden provocar resultados inesperados al leer datos de un origen de datos de Excel.  
  
-   **Orígenes de datos**. El origen de datos de un libro de Excel puede ser una hoja de cálculo, a cuyo nombre debe agregarse el signo $ (por ejemplo, Hoja1$), un rango con nombre (por ejemplo, MiRango). En una instrucción SQL, el nombre de la hoja debe estar delimitado (por ejemplo [Hoja1$]) para evitar un error de sintaxis producido por el signo $. El Generador de consultas agrega automáticamente estos delimitadores. Al especificar una hoja de cálculo o un rango, el controlador lee los bloques contiguos de celdas, comenzando con la primera celda no vacía en la esquina superior izquierda de la hoja de cálculo o rango. Por tanto, no deben dejarse filas vacías en los datos de origen, ni una fila vacía entre las filas de título o de cabecera y las filas de datos.  
  
-   **Valores que faltan**. Este controlador lee un cierto número de filas (de forma predeterminada, 8) en el origen especificado para elegir el tipo de datos de cada columna. Cuando una columna parece contener varios tipos de datos, especialmente numéricos y de texto, el controlador elige el tipo más usado y devuelve valores NULL en las celdas que contienen datos de los demás tipos. (En caso de empate, el tipo numérico tiene prioridad.) La mayoría de las opciones de formato en las hojas Excel parecen no afectar a esta determinación de tipos de datos. Para modificar este comportamiento del controlador de Excel, especifique el modo de importación. Para especificar el `IMEX=1` modo de importación, agregue al valor de Propiedades extendidas en la cadena de conexión del Administrador de conexiones de Excel en la ventana **Propiedades.** Para obtener más información, vea [PRB: valores de Excel devueltos como NULL usando DAO OpenRecordset](https://support.microsoft.com/kb/194124).  
  
-   **Texto truncado**. Cuando el controlador determina que una columna de Excel contiene datos de texto, el controlador selecciona el tipo de datos (cadena o memorando) en función del valor más largo que muestrea. Si el controlador no descubre valores de más de 255 caracteres en las filas que muestrea, trata a la columna como una columna de cadena de 255 caracteres en lugar de una columna memorando. Así, es posible que se trunquen las cadenas con más de 255 caracteres. Para importar datos de una columna memorando sin que se trunquen, debe asegurarse de que la columna memo contenga, en al menos una de las filas muestreadas, un valor superior a los 255 caracteres, o tendrá que incrementar el número de filas muestreadas por el controlador para que se incluya dicha fila. Puede aumentar el número de filas muestreadas al incrementar el valor de **TypeGuessRows** en la clave del registro **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Jet\4.0\Engines\Excel** . Para más información, vea [PRB: transferencia de datos del origen de OLEDB de Jet 4.0 con error](https://support.microsoft.com/kb/281517).  
  
-   **Tipos de datos**. El controlador de Excel reconoce solo un conjunto limitado de tipos de datos. Por ejemplo, todas las columnas numéricas se interpretan como dobles (DT_R8) y todas las columnas de cadena (a excepción de las columnas memorando) se interpretan como cadenas Unicode de 255 caracteres (DT_WSTR). [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] asigna los tipos de datos de Excel de la siguiente manera:  
  
    -   Numérico flotante de doble precisión (DT_R8)  
  
    -   Moneda: moneda (DT_CY)  
  
    -   Booleano: booleano (DT_BOOL)  
  
    -   Fecha/hora `datetime` - (DT_DATE)  
  
    -   Cadena: cadena Unicode, longitud de 255 caracteres (DT_WSTR)  
  
    -   Memorando: flujo de texto Unicode (DT_NTEXT)  
  
-   **Conversiones de tipo de datos y de longitud**. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no convierte tipos de datos de forma implícita. Como resultado, probablemente necesite utilizar las transformaciones Columna derivada o Conversión de datos para convertir datos de Excel de forma explícita antes de cargarlos en un destino diferente de Excel, o para convertir datos que no son de Excel antes de cargarlos en un destino de Excel. En este caso, puede resultar útil crear el paquete inicial a través del Asistente para importación y exportación, que le configura las conversiones necesarias. Entre algunos ejemplos de las conversiones que se pueden requerir, figuran:  
  
    -   Conversión entre columnas de cadena de Excel Unicode y columnas de cadena no Unicode con páginas de códigos específicas  
  
    -   Conversión entre columnas de cadena de Excel de 255 caracteres y columnas de cadena de diferentes longitudes  
  
    -   Conversión entre columnas numéricas de Excel de doble precisión y columnas numéricas de otros tipos  
  
## <a name="excel-source-configuration"></a>Configuración del origen de Excel  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de origen de Excel** , haga clic en uno de los temas siguientes:  
  
-   [Editor de origen de Excel &#40;página Administrador de conexiones&#41;](../excel-source-editor-connection-manager-page.md)  
  
-   [Editor de origen de Excel &#40;página Columnas&#41;](../excel-source-editor-columns-page.md)  
  
-   [Editor de origen de Excel &#40;página Salida de error&#41;](../excel-source-editor-error-output-page.md)  
  
 El cuadro de diálogo **Editor avanzado** indica todas las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](../common-properties.md)  
  
-   [Propiedades personalizadas de Excel](excel-custom-properties.md)  
  
 Para más información sobre cómo crear bucles entre un grupo de archivos de Excel, vea [Crear bucles entre archivos y tablas de Excel usando un contenedor de bucles Foreach](../control-flow/foreach-loop-container.md).  
  
## <a name="related-tasks"></a>Related Tasks  

-   [Importación de datos desde Excel o exportación de datos a Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)

-   [Asignar parámetros de consulta a variables en un componente de flujo de datos](map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [Establecer las propiedades de un componente de flujo de datos](set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordenar datos para las transformaciones Mezclar y Combinación de mezcla](transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
-   [Crear bucles entre archivos y tablas de Excel usando un contenedor de bucles Foreach](../control-flow/foreach-loop-container.md)  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Entrada de blog sobre cómo [importar datos de Excel de 64 bits en SSIS](https://go.microsoft.com/fwlink/?LinkId=217673)en hrvoje.piasevoli.com  
  
-   Entrada de blog, [Conexión a Excel (XLSX) en SSIS](https://microsoft-ssis.blogspot.com/2014/02/connecting-to-excel-xlsx-in-ssis.html).  
  
  

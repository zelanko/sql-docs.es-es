---
title: Destino de Excel | Documentos de Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.exceldest.f1
helpviewer_keywords:
- destinations [Integration Services], Excel
- Excel [Integration Services]
ms.assetid: 37c07446-1264-4814-b4f5-9c66d333bb24
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 62feb48c0b05d6f7c8d6b3342b49d9b050113ac3
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="excel-destination"></a>Destino de Excel
  El destino de Excel carga datos en hojas de cálculo o rangos en libros de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel.  
  
## <a name="access-modes"></a>Modos de acceso  
 El destino de Excel proporciona tres modos diferentes de acceso a los datos para cargar datos:  
  
-   Una tabla o vista.  
  
-   Una tabla o vista especificadas en una variable.  
  
-   Los resultados de una instrucción SQL. La consulta puede tener parámetros.  
  
> [!IMPORTANT]  
>  En Excel, una hoja o un rango equivalen a una tabla o vista. Las listas de tablas disponibles en los editores de Origen y Destino de Excel muestran solo las hojas de cálculo existentes (identificadas con el signo $ anexado al nombre de la hoja de cálculo, como, por ejemplo, Hoja1$) y rangos con nombre (identificados por la falta del signo $, como por ejemplo, MiRango).  
  
## <a name="usage-considerations"></a>Consideraciones de uso  
 El Administrador de conexiones con Excel usa el Proveedor OLE DB de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para Jet 4.0 y el controlador ISAM (Método de acceso secuencial indexado) de Excel asociado para conectar con orígenes Excel de datos y leer y escribir datos en ellos.  
  
 Muchos artículos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base documentan el comportamiento de este proveedor y el controlador. Aunque estos artículos no son específicos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ni de Servicios de transformación de datos (su predecesor), posiblemente le interese conocer determinados comportamientos que pueden provocar resultados inesperados. Para obtener información general sobre el uso y el comportamiento del controlador de Excel, vea [Cómo usar ADO con datos de Excel procedentes de Visual Basic o VBA](http://support.microsoft.com/kb/257819).  
  
 Los siguientes comportamientos del proveedor Jet que se incluye con el controlador de Excel pueden provocar resultados inesperados al guardar datos en un destino de Excel.  
  
-   **Guardar datos de texto**. Cuando el controlador de Excel guarda valores de datos de texto en un destino de Excel, el controlador precede el texto en cada celda con el carácter de comilla simple (') para garantizar que los valores guardados se interpreten como valores de texto. Si posee o desarrolla otras aplicaciones que leen o procesan los datos guardados, es posible que necesite un tratamiento especial para el carácter de comilla simple que precede cada valor de texto.  
  
     Si desea información sobre cómo evitar incluir las comillas simples, consulte esta entrada de blog, [Se añade una comilla simple a todas las cadenas al transformar los datos a Excel cuando se utiliza el componente de flujo de datos de destino Excel en un paquete SSIS](http://go.microsoft.com/fwlink/?LinkId=400876), en msdn.com.  
  
-   **Guardar datos de memorando (ntext)**. Para poder guardar correctamente cadenas de más de 255 caracteres en una columna de Excel, el controlador debe reconocer el tipo de datos de la columna de destino como **memorando** y no como **cadena**. Si la tabla de destino ya contiene filas de datos, las primeras filas que pruebe el controlador deberán contener por lo menos una instancia de un valor de más de 255 caracteres en la columna de memorando. Si la tabla de destino se crea durante el diseño del paquete o en tiempo de ejecución, la instrucción CREATE TABLE deberá utilizar LONGTEXT (o uno de sus sinónimos) como el tipo de datos de la columna de memorando.  
  
-   **Tipos de datos**. El controlador de Excel reconoce solo un conjunto limitado de tipos de datos. Por ejemplo, todas las columnas numéricas se interpretan como dobles (DT_R8) y todas las columnas de cadena (a excepción de las columnas memorando) se interpretan como cadenas Unicode de 255 caracteres (DT_WSTR). [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] asigna los tipos de datos de Excel de la siguiente manera:  
  
    -   Numérico    flotante de doble precisión (DT_R8)  
  
    -   Moneda     moneda (DT_CY)  
  
    -   Booleano     booleano (DT_BOOL)  
  
    -   Fecha y hora     **datetime** (DT_DATE)  
  
    -   Cadena    cadena Unicode, longitud de 255 caracteres (DT_WSTR)  
  
    -   Memorando     flujo de texto Unicode (DT_NTEXT)  
  
-   **Conversiones de tipo de datos y de longitud**. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no convierte tipos de datos de forma implícita. Como resultado, probablemente necesite usar las transformaciones Columna derivada o Conversión de datos para convertir datos de Excel de forma explícita antes de cargarlos en un destino diferente de Excel, o para convertir datos que no son de Excel antes de cargarlos en un destino de Excel. En este caso, puede resultar útil crear el paquete inicial a través del Asistente para importación y exportación, que le configura las conversiones necesarias. Entre algunos ejemplos de las conversiones que se pueden requerir, figuran:  
  
    -   Conversión entre columnas de cadena de Excel Unicode y columnas de cadena no Unicode con páginas de códigos específicas.  
  
    -   Conversión entre columnas de cadena de Excel de 255 caracteres y columnas de cadena de diferentes longitudes.  
  
    -   Conversión entre columnas numéricas de Excel de doble precisión y columnas numéricas de otros tipos.  
  
## <a name="configuration-of-the-excel-destination"></a>Configuración del destino de Excel  
 El destino de Excel usa un administrador de conexiones de Excel para conectarse a un origen de datos, y el administrador de conexiones especifica el archivo de libro que se debe usar. Para más información, consulte [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md).  
  
 El destino de Excel tiene una entrada normal y una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información sobre las propiedades que se pueden configurar en el cuadro de diálogo **Editor de destino de Excel** , haga clic en uno de los siguientes temas:  
  
-   [Editor de destino de Excel &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/excel-destination-editor-connection-manager-page.md)  
  
-   [Editor de destino de Excel &#40;página Asignaciones&#41;](../../integration-services/data-flow/excel-destination-editor-mappings-page.md)  
  
-   [Editor de destino de Excel &#40;página Salida de error&#41;](../../integration-services/data-flow/excel-destination-editor-error-output-page.md)  
  
 El cuadro de diálogo **Editor avanzado** indica todas las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de Excel](../../integration-services/data-flow/excel-custom-properties.md)  
  
 Para más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
-   [Conectarse a un libro de Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
-   [Crear bucles entre archivos y tablas de Excel usando un contenedor de bucles Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
-   [Establecer las propiedades de un componente de flujo de datos](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Entrada de blog, [Excel en Integration Services, parte 1 de 3: conexiones y componentes](http://go.microsoft.com/fwlink/?LinkId=217674), en dougbert.com  
  
-   Entrada de blog, [Excel en Integration Services, parte 2 de 3: tablas y tipos de datos](http://go.microsoft.com/fwlink/?LinkId=217675), en dougbert.com.  
  
-   Entrada de blog, [Excel en Integration Services, parte 3 de 3: problemas y alternativas](http://go.microsoft.com/fwlink/?LinkId=217676), en dougbert.com.  
  
## <a name="see-also"></a>Vea también  
 [Origen de Excel](../../integration-services/data-flow/excel-source.md)   
 [Integration Services &#40; SSIS &#41; Variables](../../integration-services/integration-services-ssis-variables.md)   
 [Flujo de datos](../../integration-services/data-flow/data-flow.md)   
 [Trabajar con archivos de Excel con la tarea de secuencia de comandos](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
  
  

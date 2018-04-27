---
title: Origen de archivo plano | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.flatfilesource.f1
- sql13.dts.designer.flatfilesourceadapter.connection.f1
- sql13.dts.designer.flatfilesourceadapter.columns.f1
- sql13.dts.designer.flatfilesourceadapter.errorhandling.f1
helpviewer_keywords:
- sources [Integration Services], Flat File
- text file reading [Integration Services]
- flat files
- Flat File source
ms.assetid: 4a64f7f3-f25d-4db0-93b3-a29496030e58
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: dfb8f75feeca8669f87622c895aa681121ede8f7
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="flat-file-source"></a>origen de archivo plano
  El origen de archivo plano lee datos de un archivo de texto. El archivo de texto puede tener formato delimitado, de ancho fijo o mixto.  
  
-   El formato delimitado utiliza columna y delimitadores de filas para definir columnas y filas.  
  
-   El formato de ancho fijo utiliza el ancho para definir columnas y filas. Este formato también incluye un carácter para rellenar los campos hasta alcanzar el ancho máximo.  
  
-   El formato derecho irregular utiliza el ancho para definir todas las columnas, excepto la última, que se delimita mediante el delimitador de filas.  
  
 Puede configurar el origen de archivo plano de las maneras siguientes:  
  
-   Agregue una columna a la salida de transformación que contiene el nombre del archivo de texto del que el origen de archivo plano extrae datos.  
  
-   Especifique si el origen de archivo plano interpreta las cadenas de longitud cero de las columnas como valores NULL.  
  
    > [!NOTE]  
    >  El administrador de conexiones de archivos planos utilizado por el origen de archivo plano debe configurarse para usar un formato delimitado a fin de interpretar cadenas de longitud cero como valores NULL. Si el administrador de conexiones utiliza los formatos de ancho fijo o derecho irregular, los datos que estén formados por espacios no se podrán interpretar como valores NULL.  
  
 Las columnas de salida en la salida del origen de archivo plano incluyen la propiedad FastParse. FastParse indica si la columna usa las rutinas de análisis más rápidas que no distinguen la configuración regional y permiten un análisis rápido que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona, o las rutinas de análisis estándar que sí distinguen la configuración regional. Para obtener más información, consulte [Fast Parse](http://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95) y [Standard Parse](http://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013).  
  
 Las columnas de salida también incluyen la propiedad UseBinaryFormat. Esta propiedad se usa para implementar en archivos la compatibilidad con datos binarios, como los datos con formato decimal. De forma predeterminada se establece UseBinaryFormat en **False**. Si quiere usar un formato binario, establezca UseBinaryFormat en **True** y el tipo de datos de la columna de salida en **DT_BYTES**. Al hacer esto, el origen de archivos planos omite la conversión de los datos y los pasa a la columna de salida tal y como están. A continuación, se puede usar una transformación como Columna derivada o Conversión de datos para convertir los datos **DT_BYTES** en otro tipo de datos; también se puede escribir un script personalizado en una transformación de script para interpretar los datos. Por último, también se puede escribir un componente de flujo de datos personalizado que interprete los datos. Para obtener más información sobre los tipos de datos en que se pueden convertir los datos **DT_BYTES**, vea [Conversión &#40;expresión de SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 Este origen utiliza un administrador de conexiones de archivos planos para tener acceso al archivo de texto. Si establece las propiedades del administrador de conexiones de archivos planos, puede proporcionar información sobre el archivo y cada columna que contiene, y especificar cómo debe controlar el origen de archivo plano los datos del archivo de texto. Por ejemplo, puede especificar los caracteres que delimitan columnas y filas en el archivo, así como el tipo de datos y la longitud de cada columna. Para más información, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 Este origen tiene una salida y una salida de error.  
  
## <a name="configuration-of-the-flat-file-source"></a>Configuración del origen de archivo plano  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de archivo plano](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener más detalles sobre cómo establecer las propiedades de un componente de flujo de datos, vea [Establecer las propiedades de un componente de flujo de datos](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="flat-file-source-editor-connection-manager-page"></a>Editor de origen de archivos planos (página Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de origen de archivos planos** para seleccionar el administrador de conexiones que utilizará el origen de archivos planos. El origen de archivos planos lee los datos de un archivo de texto, que pueden estar en formato delimitado, tener un ancho fijo o ser mixtos.  
  
 Un origen de archivos planos puede utilizar uno de los siguientes tipos de administradores de conexiones:  
  
-   Un administrador de conexiones de archivos planos, si el origen es un único archivo plano. Para más información, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
-   Un administrador de conexiones de varios archivos planos, si el origen son varios archivos planos y la tarea Flujo de datos se encuentra en un contenedor de bucles, como el contenedor de bucles For. En cada bucle del contenedor, el origen de archivos planos carga los datos del siguiente nombre de archivo que proporciona el administrador de conexiones de varios archivos planos. Para más información, consulte [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="options"></a>Opciones  
 **Flat file connection manager**  
 Seleccione un administrador de conexiones de la lista o cree un nuevo administrador de conexiones haciendo clic en **Nuevo**.  
  
 **Nueva**  
 Crea un nuevo administrador de conexiones mediante el cuadro de diálogo **Editor del administrador de conexiones de archivos planos** .  
  
 **Conservar los valores null del origen como valores null en el flujo de datos**  
 Especifica si deben mantenerse los valores NULL cuando se extraen los datos. El valor predeterminado de esta propiedad es **false**. Cuando este valor es f**alse**, el origen de archivos planos reemplaza los valores NULL del origen de datos por los valores predeterminados correspondientes para cada columna, como cadenas vacías para las columnas de cadenas o cero para las columnas numéricas.  
  
 **Vista previa**  
 Muestra una vista previa de los resultados mediante el cuadro de diálogo **Vista de datos** . La vista previa puede mostrar hasta 200 filas.  
  
## <a name="flat-file-source-editor-columns-page"></a>Editor de origen de archivos planos (página Columnas)
  Use el nodo **Columnas** del cuadro de diálogo **Editor de origen de archivos planos** para asignar una columna de salida a cada columna externa (origen).  
  
> [!NOTE]  
>  La propiedad **FileNameColumnName** del origen de archivo plano y la propiedad **FastParse** de sus columnas de salida no están disponibles en el **Editor de origen de archivos planos**, pero se puede establecer con el **Editor avanzado**. Para obtener más información acerca de estas propiedades, vea la sección sobre el origen de archivos planos en [Flat File Custom Properties](../../integration-services/data-flow/flat-file-custom-properties.md).  
  
### <a name="options"></a>Opciones  
 **Columnas externas disponibles**  
 Muestra la lista de columnas externas disponibles en el origen de datos. Esta tabla no se puede usar para agregar o quitar columnas.  
  
 **Columna externa**  
 Vea las columnas externas (origen) en el orden en que la tarea las leerá. Puede cambiar este orden si elimina primero las columnas seleccionadas en la tabla y luego selecciona las columnas externas de la lista en un orden diferente.  
  
 **Columna de salida**  
 Permite proporcionar un nombre único para cada columna de salida. El nombre predeterminado es el nombre de la columna externa (origen) seleccionada; sin embargo, puede elegir un nombre único y descriptivo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
## <a name="flat-file-source-editor-error-output-page"></a>Editor de origen de archivos planos (página Salida de error)
  Use la página **Salida de error** del cuadro de diálogo **Editor de origen de archivos planos** para seleccionar opciones de control de errores y establecer las propiedades en las columnas de salida de error.  
  
### <a name="options"></a>Opciones  
 **Entrada/salida**  
 Muestra el nombre del origen de datos.  
  
 **Columna**  
 Permite ver las columnas externas (origen) seleccionadas en la página **Administrador de conexiones** del cuadro de diálogo **Editor de origen de archivos planos**.  
  
 **Error**  
 Permite especificar qué debe ocurrir cuando se produce un error: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Temas relacionados:** [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Truncamiento**  
 Permite especificar qué debe ocurrir cuando se produce un truncamiento: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Descripción**  
 Muestra la descripción del error.  
  
 **Establecer este valor en las celdas seleccionadas**  
 Permite especificar qué debe ocurrir en todas las celdas seleccionadas cuando se produce un error o un truncamiento: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Aplicar**  
 Aplica la opción de control de errores a las celdas seleccionadas.  
  
## <a name="see-also"></a>Ver también  
 [Destino de archivo plano](../../integration-services/data-flow/flat-file-destination.md)   
 [Flujo de datos](../../integration-services/data-flow/data-flow.md)  
  
  

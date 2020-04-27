---
title: Editor de origen de CDC (página Administrador de conexiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsource.connection.f1
ms.assetid: 304e6717-e160-4a7b-a06f-32182449fef8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7e33946220b10f35596a6496637c8572f5b97403
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66061061"
---
# <a name="cdc-source-editor-connection-manager-page"></a>Editor de origen de CDC (página Administrador de conexiones)
  Use la página **Administrador de conexiones** del cuadro de diálogo del **Editor de origen de CDC** con el fin de seleccionar el administrador de conexiones de ADO.NET para la base de datos de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] donde el origen de CDC lee las filas de cambios (la base de datos CDC). Una vez que se haya seleccionado la base de datos CDC, debe seleccionar una tabla capturada en la base de datos.  
  
 Para obtener más información acerca del origen de CDC, vea [CDC Source](data-flow/cdc-source.md).  
  
## <a name="task-list"></a>Lista de tareas  
 **Para abrir la página Administrador de conexiones del Editor de origen de CDC**  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra el paquete [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] que tiene el origen de CDC.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el origen de CDC.  
  
3.  En el **Editor de origen de CDC**, haga clic en **Administrador de conexiones**.  
  
## <a name="options"></a>Opciones  
 **Administrador de conexiones de ADO.NET**  
 Seleccione un administrador de conexiones existente de la lista o haga clic en **Nueva** para crear una nueva conexión. Es preciso realizar la conexión a una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] habilitada para CDC y donde se encuentre la tabla de cambios seleccionada.  
  
 **Nuevo**  
 Haga clic en **Nueva**. Se abrirá el cuadro de diálogo **Configurar el administrador de conexiones ADO.NET** , donde puede crear un administrador de conexiones nuevo.  
  
 **Tabla CDC**  
 Seleccione la tabla de origen de CDC que contenga los cambios capturados que desee leer y distribuir para el procesamiento de los componentes SSIS de nivel inferior.  
  
 **Instancia de captura**  
 Seleccione o escriba el nombre de la instancia de captura CDC con la tabla CDC que se va a leer.  
  
 Una tabla de origen capturada puede tener una o dos instancias capturadas para controlar que la transición de una definición de tabla a través de los cambios en el esquema se realice sin problemas. Si se define más de una instancia de captura para la tabla de origen que se va a capturar, seleccione aquí la instancia de captura que desee usar. El nombre predeterminado de la instancia de captura para una tabla [esquema].[tabla] es \<schema>_\<table>, pero los nombres de instancia de captura reales en uso podrían ser distintos. La tabla real de la que se lee es la tabla CDC **CDC\< .>_CT de la instancia de captura**.  
  
 **Modo de procesamiento CDC**  
 Seleccione el modo de procesamiento que mejor controle las necesidades de procesamiento. Las opciones posibles son:  
  
-   **Todos**: devuelve los cambios en el intervalo CDC actual sin los valores de **Antes de actualización** .  
  
-   **Todos con valores antiguos**: devuelve los cambios en el intervalo de procesamiento CDC actual, incluidos los valores antiguos (**Antes de actualización**). Para cada operación de actualización habrá dos filas: una con los valores anteriores a la actualización y otra con los valores posteriores a la actualización.  
  
-   **Neto**: devuelve una sola fila de cambios por cada fila de origen modificada en el intervalo de procesamiento de CDC actual. Si una fila de origen se actualizó varias veces, se genera el cambio combinado (por ejemplo, se genera insertar+actualizar como una actualización única y se genera actualizar+eliminar como una eliminación única). Al trabajar en el modo de procesamiento de cambios Neto, es posible dividir los cambios en salidas de eliminar, insertar y actualizar y controlarlos todos en paralelo, ya que la fila de origen única aparece en más de un resultado.  
  
-   **Neto con máscara de actualización**: este modo es similar al modo Neto normal, pero también agrega columnas booleanas con el patrón de nombre **__$\<column-name>\__Changed** que indica las columnas modificadas en la fila de cambio actual.  
  
-   **Neto con combinación**: este modo es similar al modo Neto normal, pero con las operaciones de inserción y actualización combinadas en una sola operación de combinación (UPSERT).  
  
> [!NOTE]  
>  Para todas las opciones de cambio Neto, la tabla de origen debe tener una clave principal o un índice único. Para las tablas sin una clave principal o índices únicos, debe usar la opción **Todos** .  
  
 **Variable que contiene el estado CDC**  
 Seleccione la variable de paquete de la cadena de SSIS que mantenga el estado CDC para el contexto CDC actual. Para obtener más información sobre la variable de estado CDC, vea [Definir una variable de estado](data-flow/define-a-state-variable.md).  
  
 **Incluir una columna de indicador de reprocesamiento**  
 Active esta casilla para crear una columna especial de salida denominada **__$reprocessing**.  
  
 Esta columna tiene un valor **true** cuando el intervalo de procesamiento CDC se superpone con el intervalo de procesamiento inicial (el intervalo de LSN correspondiente al periodo de carga inicial) o cuando un intervalo de procesamiento CDC se vuelve a procesar tras un error en una ejecución anterior. Con esta columna de indicador, el desarrollador de SSIS puede controlar los errores de manera diferente a cuando se vuelven a procesar los cambios (por ejemplo, se pueden omitir acciones como la eliminación de una fila que no existe o una inserción que causó un error en una clave duplicada).  
  
 Para más información, consulte [CDC Source Custom Properties](data-flow/cdc-source-custom-properties.md).  
  
## <a name="see-also"></a>Consulte también  
 [Editor de origen de CDC &#40;página columnas&#41;](../../2014/integration-services/cdc-source-editor-columns-page.md)   
 [Editor de origen de CDC &#40;página Salida de error&#41;](../../2014/integration-services/cdc-source-editor-error-output-page.md)  
  
  

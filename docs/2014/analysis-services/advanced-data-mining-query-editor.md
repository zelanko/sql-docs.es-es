---
title: Advanced Editor de consultas de minería de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 27e7fc46-689d-43a4-9647-1c27d182bdd6
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 430a9263b15b385dd6e5f8f7aa24be15a54edffd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105038"
---
# <a name="advanced-data-mining-query-editor"></a>Editor de consultas de minería de datos avanzada
  El **datos minería Editor de consultas avanzadas** es una herramienta para ayudarle a crear consultas y modelos personalizados.  
  
 El editor proporciona un conjunto de plantillas con los vínculos en los que se puede hacer clic. Basta con hacer clic en cada vínculo y usar los cuadros de diálogo para seleccionar objetos o valores y crear instrucciones complejas de Extensiones de minería de datos (DMX). Puede cambiar la vista al modelo de edición de texto para modificar la instrucción DMX manualmente.  
  
 Para obtener la **datos minería Editor de consultas avanzadas**, haga clic en **consulta** y, a continuación, haga clic en **avanzadas**.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Panel consulta DMX**  
 Aquí puede ver la instrucción DMX actual.  
  
 Haga clic con el botón secundario en este panel para copiar la instrucción DMX actual.  
  
 También puede hacer clic en cualquier parte resaltada de la instrucción para ver las opciones específicas de esa cláusula. Por ejemplo, para eliminar, agregar o editar una salida, haga clic en el  **\<salida >** vínculo.  
  
 **Editar consulta/generador de consultas**  
 Use este botón para cambiar el editor entre un editor de texto, donde puede escribir instrucciones DMX directamente; y el **generador de consultas**, lo que ayuda a compilar una instrucción DMX.  
  
> [!NOTE]  
>  **Advertencia:** si cambia las vistas antes de que se ha ejecutado la consulta, aparece un mensaje que indica que podría perder algunos cambios. Si la instrucción DMX es válida, en muchos casos el **generador de consultas** puede convertir correctamente estos cambios. Sin embargo, si ha creado una instrucción DMX muy compleja, debe guardar el trabajo antes de cambiar de vista.  
  
 **Plantillas DMX**  
 Haga clic en esta opción y seleccione en la lista una de las plantillas que contienen los ejemplos DMX. Las plantillas proporcionan información solo sobre cada tipo de consulta de modelo o de predicción que puede necesitar, incluidas las consultas que usan tablas anidadas, e instrucciones DMX para administrar los modelos. Aunque tenga conocimientos de DMX, las plantillas pueden ahorrarle tiempo al mostrar la sintaxis correcta.  
  
 **Elija el modelo**  
 Haga clic aquí para ver una lista de los modelos de minería de datos disponibles en la conexión actual.  
  
 También puede mostrar una lista de modelos disponibles, haga clic en el nombre del modelo en la instrucción DMX en la **consulta DMX** panel. El nombre del modelo suele aparecer resaltado en rojo.  
  
 **Seleccione la entrada**  
 Haga clic en esta opción para elegir los datos que se usarán como entrada para el modelo de minería de datos. Si no se ha especificado ningún origen de datos, también puede hacer clic en el  **\<entrada >** vínculo, que aparece resaltado en rojo en el **consulta DMX** panel.  
  
 Seleccione **@InputRowset** en la lista desplegable para abrir el **reemplazar InputRowset** diálogo cuadro y modificar una entrada existente.  
  
 Seleccione **Agregar entrada** para abrir el **Agregar entrada** diálogo cuadro y especifique un nuevo origen de datos.  
  
 También puede modificar una entrada existente, haga clic en el **@InputRowset** vínculo, que aparece resaltado en rojo en el panel consulta DMX.  
  
 **Asignar columnas**  
 Seleccione columnas del modelo de minería de datos y asígnelas a columnas del origen de datos externo.  
  
 También puede hacer clic el resaltado  **\<asignación >** vínculo en el panel consulta DMX.  
  
 **Agregar salida**  
 Haga clic en esta opción para elegir las columnas que deben incluirse en la salida como parte de una consulta de predicción.  
  
 También puede hacer clic el resaltado  **\<agregar salida >** vínculo en el panel consulta DMX.  
  
 **Columnas del modelo**  
 Muestra una lista de las columnas del modelo de minería de datos seleccionado. Si aparece un símbolo en forma de rombo al lado del nombre de la columna, significa que se trata de una columna de predicción.  
  
 **Columnas de entrada**  
 Muestra una lista de las columnas del origen de datos externo que se han agregado como entradas.  
  
## <a name="see-also"></a>Vea también  
 [Consulta &#40;complementos de minería de datos de SQL Server&#41;](query-sql-server-data-mining-add-ins.md)  
  
  
---
title: Editor de consultas avanzadas de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 27e7fc46-689d-43a4-9647-1c27d182bdd6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4973ea427cea99d6e3c4527e8686e322a97efe48
ms.sourcegitcommit: c7a202af70fd16467a498688d59637d7d0b3d1f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313609"
---
# <a name="advanced-data-mining-query-editor"></a>Editor de consultas avanzadas de minería de datos
  La **consulta de minería de datos editor avanzado** es una herramienta que le ayudará a crear modelos y consultas personalizados.  
  
 El editor proporciona un conjunto de plantillas con los vínculos en los que se puede hacer clic. Basta con hacer clic en cada vínculo y usar los cuadros de diálogo para seleccionar objetos o valores y crear instrucciones complejas de Extensiones de minería de datos (DMX). Puede cambiar la vista al modelo de edición de texto para modificar la instrucción DMX manualmente.  
  
 Para ir al **editor avanzado consulta de minería de datos**, haga clic en **consulta** y, a continuación, haga clic en **avanzadas**.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Panel consulta DMX**  
 Aquí puede ver la instrucción DMX actual.  
  
 Haga clic con el botón secundario en este panel para copiar la instrucción DMX actual.  
  
 También puede hacer clic en cualquier parte resaltada de la instrucción para ver las opciones específicas de esa cláusula. Por ejemplo, para eliminar, agregar o editar una salida, haga clic con el botón secundario en el vínculo **\<Output >** .  
  
 **Editar consulta/Generador de consultas**  
 Use este botón para cambiar el editor entre un editor de texto, donde puede escribir instrucciones DMX directamente. y el **generador de consultas**, que le ayuda a crear una instrucción DMX.  
  
> [!NOTE]  
>  **Advertencia:** Si cambia de vista antes de que se haya ejecutado la consulta, aparece un mensaje que indica que podría perder algunos cambios. Si la instrucción DMX es válida, en muchos casos el **generador de consultas** podría convertir correctamente estos cambios. Sin embargo, si ha creado una instrucción DMX muy compleja, debe guardar el trabajo antes de cambiar de vista.  
  
 **Plantillas DMX**  
 Haga clic en esta opción y seleccione en la lista una de las plantillas que contienen los ejemplos DMX. Las plantillas proporcionan información solo sobre cada tipo de consulta de modelo o de predicción que puede necesitar, incluidas las consultas que usan tablas anidadas, e instrucciones DMX para administrar los modelos. Aunque tenga conocimientos de DMX, las plantillas pueden ahorrarle tiempo al mostrar la sintaxis correcta.  
  
 **Elegir modelo**  
 Haga clic aquí para ver una lista de los modelos de minería de datos disponibles en la conexión actual.  
  
 También puede mostrar una lista de modelos disponibles haciendo clic en el nombre del modelo en la instrucción DMX en el panel **consulta DMX** . El nombre del modelo suele aparecer resaltado en rojo.  
  
 **Seleccionar entrada**  
 Haga clic en esta opción para elegir los datos que se usarán como entrada para el modelo de minería de datos. Si no se ha especificado ningún origen de datos, también puede hacer clic en el vínculo **\<Input >** , que aparece resaltado en rojo en el panel **consulta DMX** .  
  
 Seleccione **\@InputRowset** en la lista desplegable para abrir el cuadro de diálogo **reemplazar InputRowset** y modificar una entrada existente.  
  
 Seleccione **Agregar entrada** para abrir el cuadro de diálogo **Agregar entrada** y especifique un nuevo origen de datos.  
  
 También puede modificar una entrada existente haciendo clic en el vínculo **\@InputRowset** , que aparece resaltado en rojo en el panel consulta DMX.  
  
 **Asignar columnas**  
 Seleccione columnas del modelo de minería de datos y asígnelas a columnas del origen de datos externo.  
  
 También puede hacer clic en el vínculo resaltado **\<Mapping >** en el panel consulta DMX.  
  
 **Agregar salida**  
 Haga clic en esta opción para elegir las columnas que deben incluirse en la salida como parte de una consulta de predicción.  
  
 También puede hacer clic en el vínculo resaltado **\<Add > de salida** en el panel consulta DMX.  
  
 **Columnas del modelo**  
 Muestra una lista de las columnas del modelo de minería de datos seleccionado. Si aparece un símbolo en forma de rombo al lado del nombre de la columna, significa que se trata de una columna de predicción.  
  
 **Columnas de entrada**  
 Muestra una lista de las columnas del origen de datos externo que se han agregado como entradas.  
  
## <a name="see-also"></a>Vea también  
 [Consulta &#40;SQL Server complementos de minería de datos&#41;](query-sql-server-data-mining-add-ins.md)  
  
  

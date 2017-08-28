---
title: "Proporcionar una consulta de origen OData en tiempo de ejecución | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bcbba7f4-6e5d-46e6-a73a-3f17d3ff376a
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: 9da1f1be0a790d01f9403d6fc05a5c1498c0ee8b
ms.contentlocale: es-es
ms.lasthandoff: 08/23/2017

---
# <a name="provide-an-odata-source-query-at-runtime"></a>Proporcionar una consulta de origen OData en tiempo de ejecución
 Puede modificar la consulta de origen OData en tiempo de ejecución mediante la adición de un *expresión* a la **[OData Source]. [ Consulta]** propiedad de la tarea flujo de datos.  
  
 Las columnas devueltas deben ser las mismas columnas que fueron devueltas en tiempo de diseño; de lo contrario, obtendrá un error cuando se ejecuta el paquete. Asegúrese de especificar las mismas columnas (en el mismo orden) cuando use la opción de consulta $select. Una alternativa más segura a la opción $select consiste en anular la selección de las columnas que no desea directamente desde la interfaz de usuario del componente de origen.  
  
 Hay varias maneras de establecer de forma dinámica el valor de consulta en tiempo de ejecución. Éstos son algunos de los métodos más frecuentes.  
  
## <a name="provide-the-query-as-a-parameter"></a>Proporciona la consulta como un parámetro  
 El siguiente procedimiento muestra cómo exponer la consulta usada por un componente de origen OData como un parámetro del paquete.  
  
1.  Haga clic con el botón secundario en **Tarea Flujo de datos** y seleccione la opción **Parametrizar…** .  
  
2.  En el **parametrizar** cuadro de diálogo, seleccione **[\<nombre del componente de origen OData >]. [ Consulta]** para **propiedad**.  
  
3.  Elija si se va a **Crear nuevo parámetro** o **Usar un parámetro existente**.  
  
4.  Si selecciona **crear nuevo parámetro**:  
  
    1.  Escriba el **nombre** y la **descripción** del parámetro.  
  
    2.  Especifique el **valor** predeterminado del parámetro.  
  
    3.  Especifique el **ámbito** (**paquete** o **proyecto**) del parámetro.  
  
    4.  Especifique si el parámetro es **obligatorio** o no  
  
5.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
## <a name="provide-the-query-with-an-expression"></a>Proporciona la consulta con una expresión
 Este método es útil cuando desea crear dinámicamente la cadena de consulta en tiempo de ejecución.
  
1.  Seleccione el **tarea flujo de datos** que contiene el **origen OData**.  
  
2.  En la ventana **Propiedades** , resalte la propiedad **Expresiones** .  
  
3.  Haga clic en el botón (puntos suspensivos) para que aparezca el **Editor de expresiones de propiedad**.  
  
4.  Seleccione la propiedad **[OData Source].[Query]** .  
  
5.  Haga clic en el botón (puntos suspensivos) para **expresión**.  
  
6.  Escriba la **expresión**.  
  
7.  Haga clic en **Aceptar**.  
  
> [!NOTE]  
> Cuando se usa este enfoque, tendrá que asegurarse de que los valores establecidos están correctamente codificada de dirección URL. Cuando reciba valores de datos proporcionados por el usuario (por ejemplo, al establecer valores de opción de consulta individuales de un parámetro), debe asegurarse de que los valores se validan para impedir posibles ataques de inyección de código SQL.  
  
  

---
title: Modificar consulta de origen OData en tiempo de ejecución | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bcbba7f4-6e5d-46e6-a73a-3f17d3ff376a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 51f92ddc8903a5c9dea9982866a22a19b013f41a
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85431982"
---
# <a name="modify-odata-source-query-at-runtime"></a>Modificar una consulta de origen OData en tiempo de ejecución
  Puede modificar la consulta de origen OData en tiempo de ejecución si agrega una expresión a la propiedad **[OData Source].[Query]** de la tarea Flujo de datos.  
  
 Tenga en cuenta que las columnas deben seguir siendo iguales que las que se usaron en tiempo de diseño; de lo contrario, obtendrá un error cuando se ejecute el paquete. Asegúrese de especificar las mismas columnas (en el mismo orden) cuando use la opción de consulta $select. Una alternativa más segura a la opción $select consiste en anular la selección de las columnas que no quiera usar directamente desde la interfaz de usuario del componente de origen.  
  
 Hay varias maneras de establecer de forma dinámica el valor de consulta en tiempo de ejecución. A continuación se muestran algunos de los métodos más frecuentes.  
  
## <a name="exposing-the-query-as-a-parameter"></a>Exponer la consulta como un parámetro  
 El procedimiento siguiente tiene pasos para exponer la consulta usada por un componente de origen OData como un parámetro del paquete.  
  
1.  Haga clic con el botón derecho en **Tarea Flujo de datos** y seleccione la opción **Parametrizar…** .  
  
2.  En el cuadro de diálogo **parametrizar** , seleccione **[ \<Name of the OData Source Component> ]. [ Consulta]** para la **propiedad**.  
  
3.  Elija si se va a **Crear nuevo parámetro** o **Usar un parámetro existente**.  
  
4.  Si selecciona **Crear nuevo parámetro**, haga lo siguiente:  
  
    1.  Escriba el **nombre** y la **descripción** del parámetro.  
  
    2.  Especifique el **valor** predeterminado del parámetro.  
  
    3.  Especifique el **ámbito** (**paquete** o **proyecto**) del parámetro.  
  
    4.  Especifique si el parámetro es **obligatorio** o no  
  
5.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
## <a name="using-an-expression"></a>Usar una expresión  
 Este método resulta útil si desea crear dinámicamente la cadena de consulta en tiempo de ejecución. En este ejemplo, la variable MaxRows se establecerá mediante otros medios (script, parámetros, etc.).  
  
1.  Seleccione la **Tarea Flujo de datos** que contiene el **Origen OData**.  
  
2.  En la ventana **Propiedades** , resalte la propiedad **Expresiones** .  
  
3.  Haga clic en... (puntos suspensivos) para abrir el editor de **expresiones de propiedad**.  
  
4.  Seleccione la propiedad **[OData Source].[Query]** .  
  
5.  Haga clic en... botón (puntos suspensivos) para **expresión**.  
  
6.  Escriba la **expresión**.  
  
7.  Haga clic en **OK**.  
  
> [!WARNING]  
>  Tenga en cuenta que cuando se usa este enfoque debe asegurarse de que los valores establecidos están codificados correctamente como una dirección URL. Cuando reciba valores de datos proporcionados por el usuario (por ejemplo, al establecer valores de opción de consulta individuales de un parámetro), debe asegurarse de que los valores se validan para impedir posibles ataques de inyección de código SQL.  
  
  

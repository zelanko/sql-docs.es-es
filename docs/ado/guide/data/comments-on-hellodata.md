---
title: Comentarios en HelloData | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: hellodata sample application [ADO]
ms.assetid: a2831d77-7040-4b73-bbae-fe0bf78107ed
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9b3cde00b3d19798d3a31b6f4c73f9b6f723e9a0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="comments-on-hellodata"></a>Comentarios en HelloData
La aplicación HelloData recorre paso a paso las operaciones básicas de una aplicación ADO típica: obtener, examinar, editar y actualizar datos. Cuando se inicia la aplicación, haga clic en el primer botón, **obtener datos**. Esto ejecutará la **GetData** subrutina.  
  
## <a name="getdata"></a>GetData  
 **GetData** coloca una cadena de conexión válida en una variable de nivel de módulo, *m_sConnStr*. Para obtener más información acerca de las cadenas de conexión, vea [crear la cadena de conexión](../../../ado/guide/data/creating-a-connection-string.md).  
  
 Asignar un controlador de errores con una Visual Basic **OnError** instrucción. Para obtener más información acerca de control de errores en ADO, vea [control de errores](../../../ado/guide/data/error-handling.md). Un nuevo **conexión** se crea el objeto y el **CursorLocation** propiedad está establecida en **adUseClient** porque el ejemplo de HelloData crea un  *conjunto de registros desconectado*. Esto significa que tan pronto como se han capturado los datos del origen de datos, se rompe la conexión física con el origen de datos, pero puede seguir trabajando con los datos que se almacena en caché localmente en su **Recordset** objeto.  
  
 Después de que se ha abierto la conexión, asigne una cadena SQL a una variable (sSQL). A continuación, cree una instancia de un nuevo **Recordset** objeto, `m_oRecordset1`. En la siguiente línea de código, abra el **Recordset** sobre existente **conexión**, pasando `sSQL` como el origen de la **conjunto de registros**. Para ayudar a ADO a tomar la determinación de que la instrucción SQL cadena que se han pasado como el origen para el **Recordset** es una definición textual de un comando pasando **adCmdText** en el argumento final de la **Open de Recordset** método. Esta línea también establece la **LockType** y **CursorType** asociados con el **conjunto de registros**.  
  
 La siguiente línea de código establece la **MarshalOptions** propiedad **adMarshalModifiedOnly**. **MarshalOptions** indica qué registros se deberían serializar en el nivel intermedio (o el servidor Web). Para obtener más información acerca de la serialización, vea la documentación de COM. Cuando usas **adMarshalModifiedOnly** con un cursor de cliente ([CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) = **adUseClient**), solo los registros que se han modificado en el cliente se reescriben en el nivel intermedio. Establecer **MarshalOptions** a **adMarshalModifiedOnly** puede mejorar el rendimiento porque se serializan menos filas.  
  
 A continuación, desconecte el **Recordset** estableciendo su **ActiveConnection** propiedad **nada**. Para obtener más información, vea la sección "Desconectar y volver a conectar el conjunto de registros" en [actualizar y conservar datos](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Cerrar la conexión al origen de datos y destruir existente **conexión** objeto. Esto libera los recursos que consumen.  
  
 El paso final consiste en establecer el **Recordset** como el **DataSource** para la cuadrícula de datos de Microsoft de Control en el formulario hasta que se pueden mostrar fácilmente los datos de la **conjunto de registros** en el formulario.  
  
 Haga clic en el segundo botón, **examinar datos**. Esta opción ejecuta la **ExamineData** subrutina.  
  
## <a name="examinedata"></a>ExamineData  
 ExamineData emplea varios métodos y propiedades de la **Recordset** objeto para mostrar información sobre los datos de la **conjunto de registros**. Indica el número de registros mediante el uso de la **RecordCount** propiedad. Recorre en bucle la **Recordset** e imprime el valor de la **AbsolutePosition** propiedad en el cuadro de texto en el formulario. Mientras se encuentre también en el bucle, el valor de la **marcador** propiedad para el tercer registro se coloca en una variable de tipo variant, *vBookmark*, para su uso posterior.  
  
 La rutina se desplaza directamente al tercer registro mediante la variable de marcador almacenada anteriormente. Las llamadas rutinarias el **WalkFields** subrutina, que recorre en bucle la **campos** colección de la **Recordset** y muestra los detalles sobre cada uno **campo**  en la colección.  
  
 Por último, **ExamineData** utiliza la **filtro** propiedad de la **Recordset** en pantalla para solo aquellos registros con un **CategoryId** igual a 2. El resultado de aplicar este filtro es inmediatamente visible en la cuadrícula de presentación en el formulario.  
  
 Para obtener más información acerca de la funcionalidad que se muestra en el **ExamineData** subrutina, vea [examinar datos](../../../ado/guide/data/examining-data.md).  
  
 A continuación, haga clic en el tercer botón, **editar datos**. Esto ejecutará la **EditData** subrutina.  
  
## <a name="editdata"></a>EditData  
 Cuando el código entra en el **EditData** subrutina, el **Recordset** sigue estando filtrado por **CategoryId** es igual a 2, para que sean de solo aquellos elementos que cumplen los criterios de filtro está visible. Recorre en primer lugar el **Recordset** y aumenta el precio de cada elemento visible en la **Recordset** 10 por ciento. El valor de la **precio** campo cambia estableciendo la **valor** propiedad para ese campo igual a una nueva cantidad válida.  
  
 Recuerde que el **Recordset** se desconecta del origen de datos. Los cambios realizados en **EditData** sólo se realizan en la copia en caché local de los datos. Para obtener más información, consulte [modificar datos](../../../ado/guide/data/editing-data.md).  
  
 Los cambios no se realizarán en el origen de datos hasta que haga clic en el cuarto botón, **actualizar datos**. Esto ejecutará la **UpdateData** subrutina.  
  
## <a name="updatedata"></a>UpdateData  
 En primer lugar, UpdateData quita el filtro que se ha aplicado a la **conjunto de registros**. El código quita y restablece `m_oRecordset1` como el **DataSource** para el control DataGrid enlazado a Microsoft en el formulario para que el sin filtrar **Recordset** aparece en la cuadrícula.  
  
 El código, a continuación, se comprueba para ver si puede moverse hacia atrás el **Recordset** mediante el uso de la **admite** método con el **adMovePrevious** argumento.  
  
 La rutina se desplaza al primer registro mediante el **MoveFirst** método y muestra los valores del campo original y actual, mediante el uso de la **OriginalValue** y **valor** propiedades de la **campo** objeto. Estas propiedades, juntas con el **UnderlyingValue** propiedad (no se utiliza aquí), se describen en [actualizar y conservar datos](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Siguiente, un nuevo **conexión** objeto se crea y se utiliza para restablecer una conexión al origen de datos. Se vuelve a conectar el **Recordset** al origen de datos estableciendo la nueva **conexión** como el **ActiveConnection** para el **conjunto de registros**. Para enviar las actualizaciones al servidor, el código llama **UpdateBatch** en el **conjunto de registros**.  
  
 Si la actualización por lotes se realiza correctamente, una variable de indicador de nivel de módulo, `m_flgPriceUpdated`, está establecida en True. Esto le recordará que más adelante para limpiar todos los cambios realizados en la base de datos.  
  
 Por último, el código se desplaza al primer registro en el **Recordset** y muestra los valores originales y actuales. Los valores son los mismos después de llamar a **UpdateBatch**.  
  
 Para obtener información detallada acerca de cómo actualizar los datos, como qué hacer cuando datos en el servidor cambia mientras su **Recordset** está desconectado, consulte [actualizar y conservar datos](../../../ado/guide/data/updating-and-persisting-data.md).  
  
## <a name="formunload"></a>Form_Unload  
 El **Form_Unload** subrutina es importante por varias razones. En primer lugar, porque se trata de una aplicación de ejemplo, Form_Unload limpia los cambios realizados en la base de datos antes de salir de la aplicación. En segundo lugar, el código muestra cómo se puede ejecutar un comando directamente desde un formato de archivo **conexión** objeto mediante el uso de la **Execute** método. Por último, se muestra un ejemplo de ejecutar una consulta no devuelve filas (una consulta UPDATE) en el origen de datos.

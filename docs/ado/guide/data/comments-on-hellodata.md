---
title: Comentarios en HelloData | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hellodata sample application [ADO]
ms.assetid: a2831d77-7040-4b73-bbae-fe0bf78107ed
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2c4897f82ff8562c031ec3522f47cddebfb56eb2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925804"
---
# <a name="comments-on-hellodata"></a>Comentarios en HelloData
Los pasos de la aplicación HelloData a través de las operaciones básicas de una aplicación típica de ADO: introducción, examinar, editar y actualizar datos. Cuando se inicia la aplicación, haga clic en el primer botón, **obtener datos**. Esto ejecutará la **GetData** subrutina.  
  
## <a name="getdata"></a>GetData  
 **GetData** coloca una cadena de conexión válida en una variable de nivel de módulo, *m_sConnStr*. Para obtener más información acerca de las cadenas de conexión, consulte [crear la cadena de conexión](../../../ado/guide/data/creating-a-connection-string.md).  
  
 Asigne un controlador de error mediante Visual Basic **OnError** instrucción. Para obtener más información sobre el control de errores en ADO, vea [Error Handling](../../../ado/guide/data/error-handling.md). Un nuevo **conexión** se crea un objeto y el **CursorLocation** propiedad está establecida en **adUseClient** porque el ejemplo de HelloData crea un  *conjunto de registros desconectado*. Esto significa que tan pronto como se han obtenido los datos del origen de datos, se interrumpe la conexión física con el origen de datos, pero puede seguir trabajando con los datos que se almacena en caché localmente en su **Recordset** objeto.  
  
 Después de que se ha abierto la conexión, asigne una cadena SQL a una variable (sSQL). A continuación, cree una instancia de un nuevo **Recordset** objeto, `m_oRecordset1`. En la siguiente línea de código, abra el **Recordset** sobre existente **conexión**, pasando `sSQL` como origen de la **Recordset**. ADO ayuda a tomar la determinación de que el código SQL cadena que se han pasado como el origen de la **Recordset** es una definición textual de un comando pasando **adCmdText** en el argumento final para el **Conjunto de registros abierto** método. Esta línea establece también el **LockType** y **CursorType** asociado con el **Recordset**.  
  
 La siguiente línea de código establece la **MarshalOptions** propiedad igual a **adMarshalModifiedOnly**. **MarshalOptions** indica qué registros se deben serializar en el nivel intermedio (o el servidor Web). Para obtener más información acerca de la serialización, vea la documentación de COM. Cuando usas **adMarshalModifiedOnly** con un cursor de cliente ([CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) = **adUseClient**), solo los registros que se han modificado en el cliente se reescriben en el nivel intermedio. Establecer **MarshalOptions** a **adMarshalModifiedOnly** puede mejorar el rendimiento porque se serializan menos filas.  
  
 A continuación, desconecte el **Recordset** estableciendo su **ActiveConnection** propiedad igual a **nada**. Para obtener más información, vea la sección "Desconectar y volver a conectar el conjunto de registros" en [actualizar y conservar datos](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Cierre la conexión al origen de datos y destruir existente **conexión** objeto. Esto libera los recursos que lo consume.  
  
 El último paso es establecer el **Recordset** como el **DataSource** para la cuadrícula de datos de Microsoft de Control del formulario hasta que se pueden mostrar fácilmente los datos de la **Recordset** en el formulario.  
  
 Haga clic en el segundo botón, **examinar datos**. Esta opción ejecuta la **ExamineData** subrutina.  
  
## <a name="examinedata"></a>ExamineData  
 ExamineData emplea varios métodos y propiedades de la **Recordset** objeto para mostrar información acerca de los datos en el **Recordset**. Informa del número de registros mediante el uso de la **RecordCount** propiedad. Recorre en bucle la **Recordset** e imprime el valor de la **AbsolutePosition** propiedad en el cuadro de texto en el formulario. Mientras se encuentre también en el bucle, el valor de la **marcador** propiedad para el tercer registro se coloca en una variable de tipo variant, *vBookmark*, para su uso posterior.  
  
 La rutina se desplaza directamente al tercer registro mediante la variable de marcador almacenada anteriormente. Las llamadas a rutinas el **WalkFields** subrutina, que recorre en bucle la **campos** colección de la **Recordset** y muestra detalles sobre cada **campo**  en la colección.  
  
 Por último, **ExamineData** usa el **filtro** propiedad de la **Recordset** en pantalla para solo aquellos registros con un **CategoryId** igual a 2. El resultado de aplicar este filtro está visible inmediatamente en la cuadrícula de presentación en el formulario.  
  
 Para obtener más información acerca de la funcionalidad que se muestra en el **ExamineData** subrutina, consulte [examinar datos](../../../ado/guide/data/examining-data.md).  
  
 A continuación, haga clic en el tercer botón, **editar datos**. Esto ejecutará la **EditData** subrutina.  
  
## <a name="editdata"></a>EditData  
 Cuando el código entra el **EditData** subrutina, el **Recordset** todavía se filtra por **CategoryId** es igual a 2, para que sean solo los elementos que cumplen los criterios de filtro está visible. Primero recorre la **Recordset** y aumenta el precio de cada elemento visible en el **Recordset** un 10 por ciento. El valor de la **precio** campo se puede cambiar estableciendo la **valor** propiedad para ese campo igual a una nueva cantidad válida.  
  
 Recuerde que el **Recordset** se desconecta del origen de datos. Los cambios que se realizaron en **EditData** sólo se realizan en la copia en caché local de los datos. Para obtener más información, consulte [modificar datos](../../../ado/guide/data/editing-data.md).  
  
 Los cambios no se realizarán en el origen de datos hasta que haga clic en el cuarto botón, **actualizar datos**. Esto ejecutará la **UpdateData** subrutina.  
  
## <a name="updatedata"></a>UpdateData  
 En primer lugar, UpdateData quita el filtro que se ha aplicado a la **Recordset**. El código quita y restablece `m_oRecordset1` como el **DataSource** para el control DataGrid enlazado a Microsoft en el formulario para que el sin filtrar **Recordset** aparece en la cuadrícula.  
  
 El código, a continuación, se comprueba para ver si puede desplazarse hacia atrás en el **Recordset** utilizando el **admite** método con el **adMovePrevious** argumento.  
  
 La rutina se mueve en el primer registro mediante el **MoveFirst** método y muestra los valores del campo original y actual, utilizando el **OriginalValue** y **valor** propiedades de la **campo** objeto. Estas propiedades, juntas con el **UnderlyingValue** propiedad (no se utiliza aquí), se tratan en [actualizar y conservar datos](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 A continuación, un nuevo **conexión** objeto se crea y se usa para restablecer una conexión al origen de datos. Se vuelve a conectar el **Recordset** al origen de datos estableciendo la nueva **conexión** como el **ActiveConnection** para el **Recordset**. Para enviar las actualizaciones al servidor, el código llama a **UpdateBatch** en el **Recordset**.  
  
 Si la actualización por lotes se realiza correctamente, una variable de indicador de nivel de módulo, `m_flgPriceUpdated`, se establece en True. Esto le recordará que más adelante para limpiar todos los cambios realizados en la base de datos.  
  
 Por último, el código se desplaza al primer registro en el **Recordset** y muestra los valores originales y actuales. Los valores son los mismos después de llamar a **UpdateBatch**.  
  
 Para obtener información detallada acerca de cómo actualizar los datos, incluido qué hacer cuando los datos en el servidor cambia mientras la **Recordset** es desconectado, consulte [actualizar y conservar datos](../../../ado/guide/data/updating-and-persisting-data.md).  
  
## <a name="formunload"></a>Form_Unload  
 El **Form_Unload** subrutina es importante por varias razones. En primer lugar, porque se trata de una aplicación de ejemplo, Form_Unload limpia los cambios realizados en la base de datos antes de salir de la aplicación. En segundo lugar, el código muestra cómo se puede ejecutar un comando directamente desde una apertura **conexión** objeto utilizando el **Execute** método. Por último, muestra un ejemplo de la ejecución de una consulta no devuelve filas (una consulta UPDATE) en el origen de datos.

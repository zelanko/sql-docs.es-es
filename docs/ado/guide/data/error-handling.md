---
title: Tratamiento de errores | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- reporting errors [ADO]
- errors [ADO]
- ADO, error handling
ms.assetid: 4909e413-f3b0-4183-8ad3-67b1434df742
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d8f96b28a15258df4b7d093ce14f227f28ad9b0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161748"
---
# <a name="error-handling"></a>Tratamiento de errores
ADO utiliza varios métodos diferentes para notificar a una aplicación de errores que se producen. Esta sección describen los tipos de errores que pueden producirse cuando se utiliza ADO y cómo se notifica a la aplicación. Concluye con sugerencias sobre cómo controlar esos errores.  
  
## <a name="how-does-ado-report-errors"></a>¿Cómo ADO notifica errores?  
 ADO notifica los errores de varias maneras:  
  
-   Errores de ADO generan un error de tiempo de ejecución. Controlar un error de ADO en la misma manera que lo haría con cualquier otro error de tiempo de ejecución, como el uso de un **On Error** instrucción en Visual Basic.  
  
-   El programa puede recibir errores de OLE DB. Error de OLE DB, genera un error de tiempo de ejecución también.  
  
-   Si el error es específico para su proveedor de datos, uno o varios **Error** objetos se colocan en el **errores** colección de la **conexión** objeto que se usó para acceder a los datos almacén cuando se produjo el error.  
  
-   Si el proceso que desencadenó un evento también generó un error, información de error se coloca en un **Error** de objetos y se pasa como parámetro al evento. Consulte [controlar eventos de ADO](../../../ado/guide/data/handling-ado-events.md) para obtener más información acerca de los eventos.  
  
-   Problemas que se producen al procesar por lotes las actualizaciones u otras operaciones masivas que implican un **Recordset** pueden ir indicados por el **estado** propiedad de la **Recordset**. Por ejemplo, pueden especificar por infracciones de restricción de esquema o no tiene permisos suficientes **RecordStatusEnum** valores.  
  
-   Problemas que se producen que implican un determinado **campo** en el registro actual también se indican mediante el **estado** propiedad de cada uno **campo** en el **campos**  colección de la **registro** o **Recordset**. Por ejemplo, se pueden especificar los tipos de datos incompatibles o las actualizaciones que no se podrían completar por **FieldStatusEnum** valores.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Errores de tiempo de ejecución de ADO](../../../ado/guide/data/ado-errors.md)  
  
-   [Errores del proveedor](../../../ado/guide/data/provider-errors.md)  
  
-   [Información de Error relacionado con el campo](../../../ado/guide/data/field-related-error-information.md)  
  
-   [Información de Error relacionado con el conjunto de registros](../../../ado/guide/data/recordset-related-error-information.md)  
  
-   [Control de errores en otros lenguajes](../../../ado/guide/data/handling-errors-in-other-languages.md)  
  
-   [Anticipación de errores](../../../ado/guide/data/anticipating-errors.md)

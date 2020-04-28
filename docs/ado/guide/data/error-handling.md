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
ms.openlocfilehash: 4cb3213b6a4c5711ccb8d6f9243047d8361a6e37
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925426"
---
# <a name="error-handling"></a>Tratamiento de errores
ADO utiliza varios métodos diferentes para notificar a una aplicación los errores que se producen. En esta sección se describen los tipos de errores que se pueden producir cuando se utiliza ADO y cómo se notifica a la aplicación. Termina realizando sugerencias sobre cómo controlar esos errores.  
  
## <a name="how-does-ado-report-errors"></a>¿Cómo se notifican los errores de ADO?  
 ADO le informa de los errores de varias maneras:  
  
-   Los errores de ADO generan un error en tiempo de ejecución. Controle un error de ADO del mismo modo que haría con cualquier otro error de tiempo de ejecución, como el uso de una instrucción **on error** en Visual Basic.  
  
-   El programa puede recibir errores de OLE DB. Un error OLE DB genera también un error en tiempo de ejecución.  
  
-   Si el error es específico del proveedor de datos, se colocan uno o varios objetos de **error** en la colección de **errores** del objeto de **conexión** que se usó para obtener acceso al almacén de datos cuando se produjo el error.  
  
-   Si el proceso que generó un evento también generó un error, la información de error se coloca en un objeto de **error** y se pasa como un parámetro al evento. Vea [control de eventos de ADO](../../../ado/guide/data/handling-ado-events.md) para obtener más información sobre los eventos.  
  
-   Los problemas que se producen al procesar actualizaciones por lotes u otras operaciones masivas que implican un **conjunto de registros** se pueden indicar mediante la propiedad **status** del **conjunto de registros**. Por ejemplo, las infracciones de la restricción de esquema o los permisos insuficientes pueden especificarse mediante los valores de **RecordStatusEnum** .  
  
-   Los problemas que se producen en un **campo** concreto del registro actual también se indican mediante la propiedad **status** de **cada campo** de la colección **Fields** del **registro** o del **conjunto de registros**. Por ejemplo, las actualizaciones que no se pudieron completar o los tipos de datos incompatibles pueden especificarse mediante los valores de **FieldStatusEnum** .  
  
 Esta sección contiene los temas siguientes.  
  
-   [Errores de tiempo de ejecución de ADO](../../../ado/guide/data/ado-errors.md)  
  
-   [Errores del proveedor](../../../ado/guide/data/provider-errors.md)  
  
-   [Información de Error relacionado con el campo](../../../ado/guide/data/field-related-error-information.md)  
  
-   [Información de Error relacionado con el conjunto de registros](../../../ado/guide/data/recordset-related-error-information.md)  
  
-   [Control de errores en otros lenguajes](../../../ado/guide/data/handling-errors-in-other-languages.md)  
  
-   [Anticipación de errores](../../../ado/guide/data/anticipating-errors.md)

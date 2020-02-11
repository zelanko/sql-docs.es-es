---
title: Estableciendo los campos de descriptor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: d735dc64-370f-48ab-a59f-6cef9bc4e1e8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 34c4a6e3d98b6711c77fb50d7156207de148881a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094255"
---
# <a name="setting-descriptor-fields"></a>Campos de Descriptor de configuración
Para modificar los campos de un descriptor, una aplicación puede llamar a **SQLSetDescField**. Algunos campos son de solo lectura y no se pueden establecer. (Consulte la descripción de la función [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) ).  
  
 Los campos de registro del descriptor se establecen con un número de registro (*RecNumber*) de 1 o superior, mientras que los campos de encabezado del descriptor se establecen con un número de registro de 0. El número de registro 0 también se usa para establecer los campos de marcador, de acuerdo con la Convención que los marcadores están contenidos en la columna 0. Esto podría dejar la impresión de que los campos de marcador están contenidos en el encabezado del descriptor, pero no es así. Los campos de marcador son distintos de los campos de encabezado.  
  
 Al establecer los campos individualmente, la aplicación debe seguir la secuencia definida en [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). La configuración de algunos campos hace que el controlador establezca otros campos. Esto garantiza que el descriptor siempre esté listo para usarse una vez que la aplicación haya especificado un tipo de datos. Cuando la aplicación establece el campo de SQL_DESC_TYPE, el controlador comprueba que otros campos que especifican el tipo son válidos y coherentes.  
  
 Si se produce un error en una llamada de función que establecería un campo descriptor, el contenido del campo descriptor no se definirá después de la llamada a la función con errores.

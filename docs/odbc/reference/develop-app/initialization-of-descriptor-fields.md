---
title: Inicialización de campos de Descriptor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- initializing descriptor fields [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1da157cb-8ea9-4a56-983b-1c45650217c5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c78162bcf0421fee609abe5fcacf9613e0f8020b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138940"
---
# <a name="initialization-of-descriptor-fields"></a>Inicialización de campos de Descriptor
Cuando se asigna un descriptor de fila de la aplicación, sus campos reciben valores iniciales como se indica en [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). El valor inicial del campo SQL_DESC_TYPE es SQL_DEFAULT. Esto proporciona un tratamiento estándar de base de datos para su presentación a la aplicación. La aplicación puede especificar un tratamiento distinto de los datos estableciendo los campos del registro de descriptor.  
  
 El valor inicial de SQL_DESC_ARRAY_SIZE en el encabezado de descriptor es 1. La aplicación puede modificar este campo para habilitar la captura de varias filas.  
  
 El concepto de un valor predeterminado no es válido para los campos de un IRD. Una aplicación puede obtener acceso a los campos de un IRD solo cuando hay una instrucción preparada o ejecutada asociada con él.  
  
 Se definen algunos de los campos de un IPD solo después de la IPD se haya rellenado automáticamente por el controlador. Si no, son indefinidos. Estos campos son SQL_DESC_CASE_SENSITIVE, SQL_DESC_FIXED_PREC_SCALE, SQL_DESC_TYPE_NAME, SQL_DESC_UNSIGNED y SQL_DESC_LOCAL_TYPE_NAME.

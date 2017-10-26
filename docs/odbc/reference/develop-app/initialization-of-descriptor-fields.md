---
title: "Inicialización de campos de Descriptor | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- initializing descriptor fields [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1da157cb-8ea9-4a56-983b-1c45650217c5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0a42ff3940f5d1620c7ee310df24016dfa39a4cd
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="initialization-of-descriptor-fields"></a>Inicialización de campos de Descriptor
Cuando se asigna un descriptor de fila de la aplicación, sus campos reciban valores iniciales como se indica en [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). El valor inicial del campo SQL_DESC_TYPE es SQL_DEFAULT. Esto proporciona un estándar tratamiento de datos de la base de datos para su presentación a la aplicación. La aplicación puede especificar un tratamiento distinto de los datos estableciendo los campos del registro del descriptor.  
  
 El valor inicial de SQL_DESC_ARRAY_SIZE en el encabezado de descriptor es 1. La aplicación puede modificar este campo para habilitar la captura de varias filas.  
  
 El concepto de un valor predeterminado no es válido para los campos de un IRD. Una aplicación puede obtener acceso a los campos de un IRD solo cuando hay una instrucción preparada o ejecutar asociada a él.  
  
 Algunos de los campos de un IPD se definen solo después de que el controlador se rellena automáticamente el IPD. Si no es así, no están definidos. Estos campos son SQL_DESC_CASE_SENSITIVE, SQL_DESC_FIXED_PREC_SCALE, SQL_DESC_TYPE_NAME, SQL_DESC_UNSIGNED y SQL_DESC_LOCAL_TYPE_NAME.


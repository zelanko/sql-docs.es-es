---
title: "Los registros de diagnóstico | Documentos de Microsoft"
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
- diagnostic information [ODBC], diagnostic records
- handles [ODBC], diagnostic records
- header records [ODBC]
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 92c73f9b-3ed7-410d-9cec-2771004aae60
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 598f047d1ae18e2c37587df270001b49d1b15831
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="diagnostic-records"></a>Registros de diagnóstico
Asociado con cada entorno, conexión, la instrucción y el identificador de descriptor son *registros de diagnóstico*. Estos registros contienen información de diagnóstico acerca de la última función llama que usa un identificador concreto. Los registros se sustituyen sólo cuando se llama a otra función con el mismo identificador. No hay ningún límite para el número de registros de diagnóstico que se pueden almacenar en cualquier momento.  
  
 Hay dos tipos de registros de diagnóstico: una *registro de encabezado* y cero o más *registros de estado*. El registro de encabezado es 0; los registros de estado son registros 1 y versiones posteriores. Los registros de diagnóstico se componen de un número de campos independientes, que son diferentes en el registro de encabezado y los registros de estado. Además, los componentes de ODBC pueden definir sus propios campos de registro de diagnóstico.  
  
 Aunque los registros de diagnóstico pueden considerarse como estructuras, no hay ningún requisito para que sean realmente estructuras; modo en que un controlador almacena la información de diagnóstico es específica del controlador.  
  
 Campos de registros de diagnóstico se recuperan con **SQLGetDiagField**. El SQLSTATE, el número de error nativo y los campos de mensaje de diagnóstico de registros de estado se pueden recuperar en una sola llamada con **SQLGetDiagRec**.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Registro de encabezado](../../../odbc/reference/develop-app/header-record.md)  
  
-   [Registros de estado](../../../odbc/reference/develop-app/status-records.md)

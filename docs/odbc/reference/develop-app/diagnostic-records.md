---
title: Registros de Diagnóstico (Diagnóstico) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- handles [ODBC], diagnostic records
- header records [ODBC]
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 92c73f9b-3ed7-410d-9cec-2771004aae60
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b564f2837bc76e04011170e191d00c08d10c119d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305186"
---
# <a name="diagnostic-records"></a>Registros de diagnóstico
Asociados a cada entorno, conexión, instrucción y identificador de descriptor son registros de *diagnóstico.* Estos registros contienen información de diagnóstico sobre la última función llamada que utiliza baña un identificador determinado. Los registros se reemplazan solo cuando se llama a otra función mediante ese identificador. No hay límite en el número de registros de diagnóstico que se pueden almacenar a la vez.  
  
 Hay dos tipos de registros de diagnóstico: un registro de *cabecera* y cero o más registros de *estado.* El registro de cabecera es el registro 0; los registros de estado son registros 1 y superiores. Los registros de diagnóstico se componen de una serie de campos independientes, que son diferentes para el registro de cabecera y los registros de estado. Además, los componentes ODBC pueden definir sus propios campos de registro de diagnóstico.  
  
 Aunque los registros de diagnóstico se pueden considerar como estructuras, no hay ningún requisito para que realmente sean estructuras; cómo un controlador almacena la información de diagnóstico es específico del controlador.  
  
 Los campos de los registros de diagnóstico se recuperan con **SQLGetDiagField**. Los campos SQLSTATE, número de error nativo y mensaje de diagnóstico de los registros de estado se pueden recuperar en una sola llamada con **SQLGetDiagRec**.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Registro de encabezado](../../../odbc/reference/develop-app/header-record.md)  
  
-   [Registros de estado](../../../odbc/reference/develop-app/status-records.md)

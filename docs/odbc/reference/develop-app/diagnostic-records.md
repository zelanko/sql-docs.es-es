---
title: Registros de diagnóstico | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 90133b4a18876c52b9b6b6bffbe4c8c02c953e07
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039882"
---
# <a name="diagnostic-records"></a>Registros de diagnóstico
Asociados con cada entorno, conexión, instrucción y identificador de descriptor son *registros de diagnóstico*. Estos registros contienen información de diagnóstico sobre la última función denominada que usó un identificador determinado. Los registros solo se sustituyen cuando se llama a otra función con ese identificador. No hay ningún límite en el número de registros de diagnóstico que se pueden almacenar en un momento dado.  
  
 Hay dos tipos de registros de diagnóstico: un *registro de encabezado* y cero o más *registros de estado*. El registro del encabezado es el registro 0; los registros de estado son registros 1 y superior. Los registros de diagnóstico se componen de varios campos independientes, que son diferentes para el registro de encabezado y los registros de estado. Además, los componentes ODBC pueden definir sus propios campos de registro de diagnóstico.  
  
 Aunque los registros de diagnóstico se pueden considerar como estructuras, no hay ningún requisito para que sean realmente estructuras; el modo en que un controlador almacena la información de diagnóstico es específico del controlador.  
  
 Los campos de los registros de diagnóstico se recuperan con **SQLGetDiagField**. Los campos SQLSTATE, número de error nativo y mensaje de diagnóstico de los registros de estado se pueden recuperar en una única llamada con **SQLGetDiagRec**.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Registro de encabezado](../../../odbc/reference/develop-app/header-record.md)  
  
-   [Registros de estado](../../../odbc/reference/develop-app/status-records.md)

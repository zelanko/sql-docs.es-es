---
title: Aplicaciones verticales ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], vertical applications
- vertical applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: d50ea3e6-7a9e-4fb6-8cd8-1d429d2f7b3c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cc88f38fd1ffe8b2ee0033ad0a2abc4f15fd5cf3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300380"
---
# <a name="vertical-applications"></a>Aplicaciones verticales
Las aplicaciones verticales suelen realizar una tarea bien definida en un único DBMS. Por ejemplo, una aplicación de entrada de pedidos realiza un seguimiento de los pedidos de una empresa. Lo que estos tipos de aplicaciones tienen en común es que el esquema de base de datos normalmente está diseñado por el desarrollador de la aplicación y, aunque la aplicación podría funcionar con un número de DBMS diferentes, funciona con un único DBMS para un solo cliente.  
  
 Dado que las aplicaciones verticales suelen requerir cierta funcionalidad, como cursores desplazables o transacciones, rara vez admiten todos los DBMS. En su lugar, tienden a ser altamente interoperables entre un conjunto limitado de DBMS. Normalmente, los desarrolladores de aplicaciones verticales eligen admitir los DBMS que representan una gran fracción del mercado e ignoran el resto. Incluso podrían optar por dar soporte a controladores específicos para esos DBMS para reducir sus costos de prueba y soporte de productos.  
  
 Dado que las aplicaciones verticales pueden admitir un conjunto conocido de DBMS, a veces contienen código específico del controlador o específico del DBMS. Sin embargo, este código se mantiene mejor al mínimo porque requiere tiempo adicional para mantener.

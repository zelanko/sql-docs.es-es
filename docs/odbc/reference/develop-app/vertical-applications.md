---
title: Aplicaciones verticales | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d0ed7a5f488765b56b2af0688ca14361590ab44
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022103"
---
# <a name="vertical-applications"></a>Aplicaciones verticales
Aplicaciones verticales suelen realizan una tarea bien definida en un único DBMS. Por ejemplo, una aplicación de entrada de pedidos realiza un seguimiento de los pedidos en una empresa. Lo que estos tipos de aplicaciones tienen en común es que normalmente se diseña el esquema de base de datos por el desarrollador de aplicaciones y, mientras que la aplicación puede funcionar con un número de diferentes DBMS, funciona con un DBMS único para un solo cliente.  
  
 Dado que las aplicaciones verticales suelen requieran cierta funcionalidad, como los cursores desplazables o transacciones, rara vez admiten todos los DBMS. En su lugar, tienden a ser muy interoperable entre un conjunto limitado de DBMS. Normalmente, los desarrolladores de aplicaciones verticales elegir admitir esos DBMS que representan una gran parte del mercado y omitir el resto. Incluso puede optar por compatibilidad con los controladores específicos de esos DBMS para reducir las pruebas y los costos de soporte técnico del producto.  
  
 Dado que las aplicaciones verticales pueden admitir un conjunto conocido de DBMS, a veces contienen código específico del controlador o específicos para DBMS. Sin embargo, dicho código mejor se reduce al mínimo porque requiere tiempo adicional para mantener.

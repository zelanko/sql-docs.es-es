---
description: Aplicaciones verticales
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a12be9247af3f273526dd08ee99ff7cc301af822
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421409"
---
# <a name="vertical-applications"></a>Aplicaciones verticales
Las aplicaciones verticales normalmente realizan una tarea bien definida en un solo DBMS. Por ejemplo, una aplicación de entrada de pedidos realiza un seguimiento de los pedidos de una empresa. Lo que tienen estos tipos de aplicaciones en común es que el esquema de la base de datos está diseñado normalmente por el desarrollador de la aplicación y, mientras que la aplicación puede funcionar con varios DBMS diferentes, funciona con un solo DBMS para un solo cliente.  
  
 Dado que las aplicaciones verticales normalmente requieren cierta funcionalidad, como cursores o transacciones desplazables, rara vez admiten todos los DBMS. En su lugar, tienden a ser altamente interoperables entre un conjunto limitado de DBMS. Normalmente, los desarrolladores de aplicaciones verticales optan por admitir los DBMS que representan una gran parte del mercado y omitir el resto. Incluso pueden optar por admitir controladores específicos para dichos DBMS con el fin de reducir sus costos de pruebas y de soporte técnico.  
  
 Dado que las aplicaciones verticales pueden admitir un conjunto conocido de DBMS, a veces contienen código específico del controlador o específico del DBMS. Sin embargo, este código se mantiene como mínimo, ya que requiere un tiempo adicional para el mantenimiento.

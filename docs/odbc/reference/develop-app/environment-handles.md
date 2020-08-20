---
description: Identificadores de entorno
title: Identificadores de entorno | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment handles [ODBC]
- handles [ODBC], environment
ms.assetid: 917f1b0c-272b-4e37-a1f5-87cd24b9fa21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1aa22a89288f4dd5a8400484078f57b60fc135fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461507"
---
# <a name="environment-handles"></a>Identificadores de entorno
Un *entorno* es un contexto global en el que se obtiene acceso a los datos; asociados a un entorno es cualquier información global por naturaleza, como:  
  
-   Estado del entorno  
  
-   Los diagnósticos actuales en el nivel de entorno  
  
-   Los identificadores de las conexiones asignadas actualmente en el entorno  
  
-   La configuración actual de cada atributo de entorno  
  
 Dentro de un fragmento de código que implementa ODBC (el administrador de controladores o un controlador), un identificador de entorno identifica una estructura que contiene esta información.  
  
 Los identificadores de entorno no se usan con frecuencia en aplicaciones ODBC. Siempre se usan en las llamadas a **SQLDataSources** y **SQLDrivers** y, a veces, se usan en llamadas a **SQLAllocHandle**, **SQLEndTran**, **SQLFreeHandle**, **SQLGetDiagField**y **SQLGetDiagRec**.  
  
 Cada fragmento de código que implementa ODBC (el administrador de controladores o un controlador) contiene uno o más identificadores de entorno. Por ejemplo, el administrador de controladores mantiene un identificador de entorno independiente para cada aplicación que está conectada a él. Los identificadores de entorno se asignan con **SQLAllocHandle** y se liberan con **SQLFreeHandle**.

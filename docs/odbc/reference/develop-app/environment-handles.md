---
title: Manijas de medio ambiente ? Microsoft Docs
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
ms.openlocfilehash: b504995e99dfad032598485e370b4d5a6681ae81
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300445"
---
# <a name="environment-handles"></a>Identificadores de entorno
Un *entorno* es un contexto global en el que acceder a los datos; asociado con un entorno es cualquier información de naturaleza global, como:  
  
-   El estado del medio ambiente  
  
-   El diagnóstico actual a nivel de entorno  
  
-   Los identificadores de las conexiones actualmente asignadas en el entorno  
  
-   La configuración actual de cada atributo de entorno  
  
 Dentro de un fragmento de código que implementa ODBC (el Administrador de controladores o un controlador), un identificador de entorno identifica una estructura que contiene esta información.  
  
 Los identificadores de entorno no se usan con frecuencia en aplicaciones ODBC. Siempre se usan en llamadas a **SQLDataSources** y **SQLDrivers** y, a veces, se usan en llamadas a **SQLAllocHandle**, **SQLEndTran**, **SQLFreeHandle**, **SQLGetDiagField**y **SQLGetDiagRec**.  
  
 Cada fragmento de código que implementa ODBC (el Administrador de controladores o un controlador) contiene uno o varios identificadores de entorno. Por ejemplo, el Administrador de controladores mantiene un identificador de entorno independiente para cada aplicación que está conectada a él. Los identificadores de entorno se asignan con **SQLAllocHandle** y se liberan con **SQLFreeHandle**.

---
title: Módulos de SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL modules [ODBC]
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], modules
- modules [ODBC]
- SQL statements [ODBC], modules
ms.assetid: 07551472-87ee-4765-951f-1364ed32f0c0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1b5cef56cec30e5ad09500135e05884bf55d5dde
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076225"
---
# <a name="sql-modules"></a>Módulos SQL
La segunda técnica para enviar instrucciones SQL para el DBMS es a través de módulos. En pocas palabras, un módulo consta de un grupo de procedimientos, que se llaman desde el host de lenguaje de programación. Cada procedimiento contiene una única instrucción SQL y datos se pasan a través de parámetros a y desde el procedimiento.  
  
 Un módulo puede considerarse como una biblioteca de objetos que esté vinculada al código de aplicación. Sin embargo, exactamente cómo los procedimientos y el resto de la aplicación se vinculan es depende de la implementación. Por ejemplo, los procedimientos podrían ser compilados en el código de objeto y vinculados directamente al código de aplicación, podría ser compilados y almacenan en el DBMS y las llamadas para tener acceso a los identificadores de plan colocados en el código de aplicación, o podrían interpretarse en tiempo de ejecución.  
  
 La ventaja principal de módulos es que separar hábilmente los problemas instrucciones SQL desde el lenguaje de programación. En teoría, debe ser posible cambiar una aplicación sin cambiar el otro y basta con volver a vincular.

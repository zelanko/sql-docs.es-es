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
manager: craigg
ms.openlocfilehash: 30c116878049c4f6a8f36e988731ab641e03c6d7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47834753"
---
# <a name="sql-modules"></a>Módulos SQL
La segunda técnica para enviar instrucciones SQL para el DBMS es a través de módulos. En pocas palabras, un módulo consta de un grupo de procedimientos, que se llaman desde el host de lenguaje de programación. Cada procedimiento contiene una única instrucción SQL y datos se pasan a través de parámetros a y desde el procedimiento.  
  
 Un módulo puede considerarse como una biblioteca de objetos que esté vinculada al código de aplicación. Sin embargo, exactamente cómo los procedimientos y el resto de la aplicación se vinculan es depende de la implementación. Por ejemplo, los procedimientos podrían ser compilados en el código de objeto y vinculados directamente al código de aplicación, podría ser compilados y almacenan en el DBMS y las llamadas para tener acceso a los identificadores de plan colocados en el código de aplicación, o podrían interpretarse en tiempo de ejecución.  
  
 La ventaja principal de módulos es que separar hábilmente los problemas instrucciones SQL desde el lenguaje de programación. En teoría, debe ser posible cambiar una aplicación sin cambiar el otro y basta con volver a vincular.

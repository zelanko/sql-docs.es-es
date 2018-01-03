---
title: "Los módulos SQL | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL modules [ODBC]
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], modules
- modules [ODBC]
- SQL statements [ODBC], modules
ms.assetid: 07551472-87ee-4765-951f-1364ed32f0c0
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aac70e91e91277f7778fed439f68e5620f116d41
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sql-modules"></a>Módulos SQL
La segunda técnica para enviar instrucciones SQL en el DBMS es a través de módulos. En pocas palabras, un módulo consta de un grupo de procedimientos, que se llaman desde el host de lenguaje de programación. Cada procedimiento contiene una sola instrucción SQL y datos se pasan hacia y desde el procedimiento a través de parámetros.  
  
 Un módulo puede considerarse como una biblioteca de objetos que se vincula al código de aplicación. Sin embargo, exactamente cómo los procedimientos y el resto de la aplicación se vinculan es depende de la implementación. Por ejemplo, los procedimientos pudieron compilados en el código de objeto o vinculados directamente en el código de aplicación, podría ser compilados y almacenados en el DBMS y las llamadas a tener acceso a identificadores de plan que se colocan en el código de aplicación, o podría interpretarse en tiempo de ejecución.  
  
 La ventaja principal de los módulos es que limpiamente independientes instrucciones SQL a partir del lenguaje de programación. En teoría, debe ser posible cambiar una aplicación sin cambiar el otro y basta con volver a vincular.

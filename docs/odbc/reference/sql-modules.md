---
title: Módulos SQL (MÓDULOs) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 351d1c6a34413b385bd76dfebb009b34c4c0f150
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280434"
---
# <a name="sql-modules"></a>Módulos SQL
La segunda técnica para enviar instrucciones SQL al DBMS es a través de módulos. Brevemente, un módulo consta de un grupo de procedimientos, que se llaman desde el lenguaje de programación host. Cada procedimiento contiene una sola instrucción SQL y los datos se pasan a y desde el procedimiento a través de parámetros.  
  
 Un módulo se puede considerar como una biblioteca de objetos que está vinculada al código de la aplicación. Sin embargo, exactamente cómo se vinculan los procedimientos y el resto de la aplicación depende de la implementación. Por ejemplo, los procedimientos podrían compilarse en código de objeto y vincularse directamente al código de la aplicación, podrían compilarse y almacenarse en el DBMS y las llamadas a los identificadores del plan de acceso colocados en el código de la aplicación, o podrían interpretarse en tiempo de ejecución.  
  
 La principal ventaja de los módulos es que separan limpiamente las instrucciones SQL del lenguaje de programación. En teoría, debería ser posible cambiar uno sin cambiar el otro y simplemente volver a vincularlos.

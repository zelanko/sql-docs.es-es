---
title: Controladores basados en archivo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
- drivers [ODBC], file-based drivers
ms.assetid: d92e0c5c-d176-4282-bbe1-d449e2223d50
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 803da51c8507faa47f92b295d3749f00317bc413
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915384"
---
# <a name="file-based-drivers"></a>Controladores basados en archivos
Controladores basados en archivos se utilizan con orígenes de datos como dBASE que no proporcionan un motor de base de datos independiente para que use el controlador. Estos controladores acceder directamente a los datos físicos y deben implementar un motor de base de datos para procesar instrucciones SQL. Como práctica estándar, los motores de base de datos en los controladores basados en archivos implementan el subconjunto de ODBC SQL definida por el nivel de conformidad mínimo de SQL; Para obtener una lista de las instrucciones SQL en este nivel de cumplimiento, consulte [Apéndice C: Gramática de SQL](../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 En comparación controladores basados en DBMS y basados en archivos, controladores basados en archivos son menos eficaces y más difícil de escribir debido al componente del motor de base de datos, menos complicado de configurar, ya que no hay partes de la red, dado que algunas personas tienen tiempo para escribir base de datos motores tan eficaces como los generados por las compañías de la base de datos.  
  
 La ilustración siguiente muestra dos configuraciones distintas de controladores basados en archivos, uno en el que residen localmente los datos y el otro en el que reside en un servidor de archivos de red.  
  
 ![Las dos configuraciones de archivo&#45;en función de los controladores](../../odbc/reference/media/pr06.gif "pr06")

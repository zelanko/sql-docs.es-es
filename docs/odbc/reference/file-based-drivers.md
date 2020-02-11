---
title: Controladores basados en archivos | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915384"
---
# <a name="file-based-drivers"></a>Controladores basados en archivos
Los controladores basados en archivos se usan con orígenes de datos como dBASE que no proporcionan un motor de base de datos independiente para que los utilice el controlador. Estos controladores acceden directamente a los datos físicos y deben implementar un motor de base de datos para procesar instrucciones SQL. Como práctica estándar, los motores de base de datos de los controladores basados en archivos implementan el subconjunto de SQL ODBC definido por el nivel de conformidad mínimo de SQL. para obtener una lista de las instrucciones SQL en este nivel de cumplimiento, vea [Apéndice C: gramática de SQL](../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 En comparación con los controladores basados en archivos y DBMS, los controladores basados en archivos son más difíciles de escribir debido al componente del motor de base de datos, menos complicado de configurar porque no hay ninguna pieza de red y menos eficaz, ya que pocas personas tienen el tiempo necesario para escribir la base de datos motores tan eficaces como los producidos por las empresas de bases de datos.  
  
 En la ilustración siguiente se muestran dos configuraciones diferentes de controladores basados en archivos, uno en el que los datos residen localmente y el otro en el que residen en un servidor de archivos de red.  
  
 ![Dos configuraciones de controladores basados en&#45;de archivos](../../odbc/reference/media/pr06.gif "pr06")

---
title: Controladores basados en archivos (File-Based Drivers) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 223bd838754f1d656ac71ae37926389097af3ea1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306668"
---
# <a name="file-based-drivers"></a>Controladores basados en archivos
Los controladores basados en archivos se utilizan con orígenes de datos como dBASE que no proporcionan un motor de base de datos independiente para que el controlador lo use. Estos controladores tienen acceso a los datos físicos directamente y deben implementar un motor de base de datos para procesar instrucciones SQL. Como práctica estándar, los motores de base de datos en controladores basados en archivos implementan el subconjunto de ODBC SQL definido por el nivel mínimo de conformidad sql; Para obtener una lista de las instrucciones SQL en este nivel de conformidad, vea [Apéndice C: Gramática SQL](../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Al comparar controladores basados en archivos y DBMS, los controladores basados en archivos son más difíciles de escribir debido al componente del motor de base de datos, menos complicado de configurar porque no hay piezas de red y menos potentes porque pocas personas tienen tiempo para escribir motores de base de datos tan potentes como los producidos por las empresas de base de datos.  
  
 En la ilustración siguiente se muestran dos configuraciones diferentes de controladores basados en archivos, una en la que los datos residen localmente y la otra en la que residen en un servidor de archivos de red.  
  
 ![Dos configuraciones de controladores basados en&#45;de archivos](../../odbc/reference/media/pr06.gif "pr06")

---
title: Crear y abrir tablas (controlador de archivo de texto) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- text file driver [ODBC], creating and opening tables
ms.assetid: e6a07dda-a665-4f5b-a8d6-9ff479700513
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 374a234f7c0f9eecc119e36d7dd4305a32745786
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="creating-and-opening-tables-text-file-driver"></a>Crear y abrir tablas (controlador de archivo de texto)
Cuando se utiliza el controlador de texto, se crea una nueva tabla con el formato especificado en Odbcinst.ini. Si no se especifica, se crean tablas en formato CSVDELIMITED. De forma predeterminada, las columnas de enteros como valor predeterminado de 11 caracteres y columnas de tipo FLOAT predeterminada a 22 caracteres. Columnas de fecha y utilice el formato aaaa-MM-DD. CHAR y columnas LONGCHAR son el ancho especificado en la instrucción CREATE.

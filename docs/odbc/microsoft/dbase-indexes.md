---
title: Índices de dBASE | Documentos de Microsoft
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
- DBase indexes [ODBC]
- DBase driver [ODBC], indexes
ms.assetid: fdfa56f5-e324-4ec2-9267-fdf95ab99373
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2d518a6f778a40c8176eed14253c12f8d743e2be
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="dbase-indexes"></a>Índices de dBASE
El controlador ODBC dBASE automáticamente abre y actualiza los archivos de índice de dBASE IV. Debe utilizar el **Seleccionar índices** cuadro de diálogo mediante el Administrador de orígenes de datos de ODBC para asociar archivos dBASE III .ndx con archivos dBASE.  
  
 Las siguientes limitaciones se aplican a la creación de índices de dBASE:  
  
-   Todos los nombres de columna deben ser válidos.  
  
-   Todas las columnas deben estar en la misma disposición ascendente o descendente.  
  
-   La longitud de cualquier columna de texto debe ser inferior a 100 bytes.  
  
-   Si existe más de una columna, todas las columnas deben ser columnas de texto y la suma de los tamaños de columna debe ser inferior a 100 bytes.  
  
-   No se puede indizar los campos de memorando.  
  
-   No se debe especificar un índice para el conjunto actual de campos (es decir, no se permiten índices duplicados).  
  
-   El nombre del índice debe coincidir con la convención de nomenclatura de índice de dBASE. dBASE III requiere que cada índice esté en un archivo independiente, cada uno con una extensión .ndx. En dBASE IV, los índices se crean como nombres de etiqueta que se almacenan en un archivo único .mdx. El archivo .mdx tiene el mismo nombre base que el archivo de base de datos (por ejemplo, Emp.mdx es el archivo de índice para la base de datos de Emp.dbf).  
  
-   dBASE define un índice único como uno donde se agrega un solo registro de un conjunto de valores clave idénticos al índice.

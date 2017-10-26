---
title: "Índices de dBASE | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DBase indexes [ODBC]
- DBase driver [ODBC], indexes
ms.assetid: fdfa56f5-e324-4ec2-9267-fdf95ab99373
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9f2725f312691d3cb644f9a096b5f469f1356c55
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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


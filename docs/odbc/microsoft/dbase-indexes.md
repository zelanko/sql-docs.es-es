---
title: Índices de dBASE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase indexes [ODBC]
- DBase driver [ODBC], indexes
ms.assetid: fdfa56f5-e324-4ec2-9267-fdf95ab99373
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9300a38a0e36da771a238f73b77d3dda527334ae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307676"
---
# <a name="dbase-indexes"></a>Índices de dBASE
El controlador ODBC dBASE abre y actualiza automáticamente los archivos de índice de dBASE IV. Debe usar el cuadro de diálogo **seleccionar índices** que se muestra a través del administrador de orígenes de datos ODBC para asociar los archivos dBase III. NDX a los archivos dBase.  
  
 Las siguientes limitaciones se aplican a la creación de índices dBASE:  
  
-   Todos los nombres de columna deben ser válidos.  
  
-   Todas las columnas deben estar en el mismo orden ascendente o descendente.  
  
-   La longitud de cualquier columna de texto individual debe ser inferior a 100 bytes.  
  
-   Si existe más de una columna, todas las columnas deben ser columnas de texto y la suma de los tamaños de columna debe ser inferior a 100 bytes.  
  
-   Los campos memo no se pueden indizar.  
  
-   No se debe especificar un índice para el conjunto actual de campos (es decir, no se permiten índices duplicados).  
  
-   El nombre del índice debe coincidir con la Convención de nomenclatura de los índices de dBASE. dBASE III requiere que cada índice esté en un archivo independiente, cada uno con una extensión. ndx. En dBASE IV, los índices se crean como nombres de etiqueta que se almacenan en un único archivo. MDX. El archivo. MDX tiene el mismo nombre base que el archivo de base de datos (por ejemplo, EMP. MDX es el archivo de índice de la base de datos EMP. dbf).  
  
-   dBASE define un índice único como uno donde solo se agrega al índice un registro de un conjunto con valores de clave idénticos.

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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d9a0a57c3dce920c6d5fbc2510932066cb5a2659
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096358"
---
# <a name="dbase-indexes"></a>Índices de dBASE
El controlador ODBC dBASE automáticamente abre y actualiza los archivos de índice de dBASE IV. Debe usar el **Seleccionar índices** cuadro de diálogo muestra mediante el Administrador de origen de datos de ODBC para asociar los archivos de dBASE III ndx archivos dBASE.  
  
 Las siguientes limitaciones se aplican a la creación de índices de dBASE:  
  
-   Todos los nombres de columna deben ser válidos.  
  
-   Todas las columnas deben estar en la misma disposición ascendente o descendente.  
  
-   La longitud de cualquier columna de texto debe ser inferior a 100 bytes.  
  
-   Si existe más de una columna, todas las columnas deben ser columnas de texto y la suma de los tamaños de columna debe ser inferior a 100 bytes.  
  
-   No se puede indizar los campos de memorando.  
  
-   No se debe especificar un índice para el conjunto de campos actual (es decir, no se permiten índices duplicados).  
  
-   El nombre del índice debe coincidir con la convención de nomenclatura del índice de dBASE. dBASE III requiere que cada índice esté en un archivo independiente, cada uno con una extensión ndx. En dBASE IV, los índices se crean como nombres de etiqueta que se almacenan en un archivo .mdx único. El archivo .mdx tiene el mismo nombre base que el archivo de base de datos (por ejemplo, Emp.mdx es el archivo de índice para la base de datos Emp.dbf).  
  
-   dBASE define un índice único como uno donde sólo un registro de un conjunto con idénticos valores de clave se agrega al índice.

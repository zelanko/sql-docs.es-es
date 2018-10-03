---
title: Funciones de catálogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], about catalog functions
- data dictionary [ODBC]
- catalog functions [ODBC]
- functions [ODBC], catalog functions
ms.assetid: 81ba9453-c085-47c0-b411-90ca6a5ee428
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 268d5f00d787cef8dfdcb29bd9e091f81a5ed2c9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692173"
---
# <a name="catalog-functions"></a>Funciones de catálogo
Todas las bases de datos tienen una estructura que describe cómo se almacenarán los datos en la base de datos. Por ejemplo, una base de datos de pedidos de ventas simple podría tener la estructura que se muestra en la ilustración siguiente, en el que se utilizan las columnas ID para vincular las tablas.  
  
 ![Muestra la estructura de una base de datos simple](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 Esta estructura, junto con otra información de privilegios, se almacena en un conjunto de tablas del sistema que llama a la base de datos *catálogo,* también conocido como un *diccionario de datos*.  
  
 Una aplicación puede detectar esta estructura a través de las llamadas a la *funciones de catálogo*. Las funciones de catálogo devuelven información en conjuntos de resultados y se suele implementa a través de **seleccione** instrucciones en las tablas en el catálogo. Por ejemplo, una aplicación puede solicitar un conjunto de resultados que contenga información sobre todas las tablas del sistema o todas las columnas de una tabla determinada.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Usos de los datos del catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [Funciones de catálogo de ODBC](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)

---
description: Funciones de catálogo
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b75e6a40252f06f6b9e2105bd557fd35ded9243f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465947"
---
# <a name="catalog-functions"></a>Funciones de catálogo
Todas las bases de datos tienen una estructura que describe cómo se almacenarán los datos en la base de datos. Por ejemplo, una base de datos simple de pedidos de ventas podría tener la estructura que se muestra en la ilustración siguiente, en la que las columnas de ID. se utilizan para vincular las tablas.  
  
 ![Muestra la estructura de una base de datos simple](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 Esta estructura, junto con otra información, como los privilegios, se almacena en un conjunto de tablas del sistema denominado Catálogo de la base de datos *,* que también se conoce como *Diccionario de datos*.  
  
 Una aplicación puede detectar esta estructura a través de llamadas a las *funciones de catálogo*. Las funciones de catálogo devuelven información en los conjuntos de resultados y normalmente se implementan mediante instrucciones **Select** en las tablas del catálogo. Por ejemplo, una aplicación puede solicitar un conjunto de resultados que contenga información sobre todas las tablas del sistema o todas las columnas de una tabla determinada.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Usos de los datos del catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [Funciones de catálogo de ODBC](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)

---
title: Funciones del catálogo ? Microsoft Docs
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
ms.openlocfilehash: eb28ec6f4ea299dae8737fc707fd53e4d102442d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305206"
---
# <a name="catalog-functions"></a>Funciones de catálogo
Todas las bases de datos tienen una estructura que describe cómo se almacenarán los datos en la base de datos. Por ejemplo, una base de datos de pedidos de ventas simple puede tener la estructura que se muestra en la siguiente ilustración, en la que se usan las columnas de identificador para vincular las tablas.  
  
 ![Muestra la estructura de una base de datos simple](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 Esta estructura, junto con otra información como privilegios, se almacena en un conjunto de tablas del sistema denominado catálogo de la base de *datos,* que también se conoce como diccionario de *datos.*  
  
 Una aplicación puede detectar esta estructura mediante llamadas a las funciones de *catálogo.* Las funciones de catálogo devuelven información en conjuntos de resultados y normalmente se implementan a través de instrucciones **SELECT** en las tablas del catálogo. Por ejemplo, una aplicación puede solicitar un conjunto de resultados que contenga información sobre todas las tablas del sistema o todas las columnas de una tabla determinada.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Usos de los datos del catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [Funciones de catálogo de ODBC](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)

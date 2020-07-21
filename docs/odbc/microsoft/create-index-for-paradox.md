---
title: CREAR índice para Paradox | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- Paradox driver [ODBC], create index
ms.assetid: 6472bd69-b931-4bc2-a9bf-f1873ed4cdfe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2e68484efdc5194f93f2acab31973377d9c66f1c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280915"
---
# <a name="create-index-for-paradox"></a>CREAR el índice de Paradox
La sintaxis de la instrucción CREATE INDEX para el controlador ODBC Paradox es la siguiente:  
  
 **Create** [**Unique**] **index** *index-Name*  
  
 **En** *nombre de tabla*  
  
 **(** *identificador de columna* [**ASC**]  
  
 [**,** *identificador de columna* [**ASC**]...] **)**  
  
 El controlador ODBC Paradox no admite la palabra clave **DESC** en la gramática SQL de ODBC para la instrucción CREATE index. El argumento de *nombre de tabla* puede especificar la ruta de acceso completa de la tabla.  
  
 Si se especifica la palabra clave **Unique** , el controlador ODBC de Paradox creará un índice único. El primer índice único se crea como índice principal. Se trata de un archivo de clave principal *de Paradox denominado Table-Name*. Píxeles. Los índices principales están sujetos a las siguientes restricciones:  
  
-   El índice principal debe crearse antes de que se agreguen filas a la tabla.  
  
-   Un índice principal debe definirse en las primeras "n" columnas de una tabla.  
  
-   Solo se permite un índice principal por tabla.  
  
-   Un controlador de Paradox no puede actualizar una tabla si no se ha definido un índice principal en la tabla. (Tenga en cuenta que esto no es cierto para una tabla vacía, que se puede actualizar aunque no se haya definido un índice único en la tabla).  
  
-   El argumento de *nombre de índice* de un índice principal debe ser el mismo que el nombre base de la tabla, tal como requiere Paradox.  
  
 Si se omite la palabra clave **Unique** , el controlador ODBC de Paradox creará un índice no único. Consta de dos archivos de índice secundarios de Paradox denominados *nombre de tabla*. X*nn* y *nombre de tabla*. Y*nn*, donde *nn* es el número de la columna de la tabla. Los índices no únicos están sujetos a las siguientes restricciones:  
  
-   Antes de que se pueda crear un índice no único para una tabla, debe existir un índice principal para esa tabla.  
  
-   Para Paradox 3. *x*, el argumento de *nombre de índice* de cualquier índice que no sea un índice principal (único o no único) debe ser el mismo que el nombre de la columna. Para Paradox 4. *x* y 5. *x*, el nombre de este tipo de índice puede ser, pero no tiene que ser igual que el nombre de la columna.  
  
-   Solo se puede especificar una columna para un índice no único.  
  
 No se pueden agregar columnas una vez que se ha definido un índice en una tabla. Si la primera columna de la lista de argumentos de una instrucción CREATE TABLE crea un índice, no se puede incluir una segunda columna en la lista de argumentos.  
  
 Por ejemplo, para usar las columnas número de pedido de ventas y número de línea como índice único en la tabla SO_LINES, use la instrucción:  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 Para usar la columna de número de pieza como índice no único en la tabla SO_LINES, use la instrucción:  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 Tenga en cuenta que, cuando se realizan dos instrucciones CREATE INDEX, la primera instrucción creará siempre un índice principal con el mismo nombre que la tabla y la segunda instrucción siempre creará un índice no único con el mismo nombre que la columna. Estos índices se denominarán de esta manera incluso si se especifican nombres diferentes en las instrucciones CREATE INDEX e incluso si el índice tiene la etiqueta UNIQUE en la segunda instrucción CREATE INDEX.  
  
> [!NOTE]  
>  Cuando se usa el controlador de Paradox sin implementar el Motor de base de datos de Borland, solo se permiten las instrucciones Read y Append.

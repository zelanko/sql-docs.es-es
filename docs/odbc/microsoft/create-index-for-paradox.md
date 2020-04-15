---
title: CREATE INDEX para Paradox ? Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280915"
---
# <a name="create-index-for-paradox"></a>CREAR el índice de Paradox
La sintaxis de la instrucción CREATE INDEX para el controlador ODBC Paradox es:  
  
 **CREATE** [**UNIQUE**] **INDEX** *index-name*  
  
 **ON** *nombre-mesa*  
  
 **(** *identificador de columna* [**ASC**]  
  
 [**,** *identificador de columna* [**ASC**]...] **)**  
  
 El controlador ODBC Paradox no admite la palabra clave **DESC** en la gramática SQL de ODBC para la instrucción CREATE INDEX. El argumento *table-name* puede especificar la ruta de acceso completa de la tabla.  
  
 Si se especifica la palabra clave **UNIQUE,** el controlador ODBC Paradox creará un índice único. El primer índice único se crea como un índice principal. Se trata de un archivo de clave principal de Paradox denominado *nombre-tabla*. Px. Los índices primarios están sujetos a las siguientes restricciones:  
  
-   El índice principal debe crearse antes de que se agreguen filas a la tabla.  
  
-   Un índice principal debe definirse en las primeras columnas "n" de una tabla.  
  
-   Solo se permite un índice principal por tabla.  
  
-   El controlador Paradox no puede actualizar una tabla si no se define un índice principal en la tabla. (Tenga en cuenta que esto no es cierto para una tabla vacía, que se puede actualizar incluso si no se define un índice único en la tabla.)  
  
-   El argumento *index-name* para un índice principal debe ser el mismo que el nombre base de la tabla, según lo requiera Paradox.  
  
 Si se omite la palabra clave **UNIQUE,** el controlador ODBC Paradox creará un índice no único. Se compone de dos archivos de índice secundario paradox denominados *nombre-tabla*. X*nn* y *nombre-tabla*. Y*nn*, donde *nn* es el número de la columna de la tabla. Los índices no únicos están sujetos a las siguientes restricciones:  
  
-   Antes de que se pueda crear un índice no único para una tabla, debe existir un índice principal para esa tabla.  
  
-   Para Paradox 3. *x*, el argumento *index-name* para cualquier índice que no sea un índice principal (único o no único) debe ser el mismo que el nombre de columna. Para Paradox 4. *x* y 5. *x*, el nombre de dicho índice puede ser, pero no tiene que ser, el mismo que el nombre de la columna.  
  
-   Solo se puede especificar una columna para un índice no único.  
  
 Las columnas no se pueden agregar una vez que se ha definido un índice en una tabla. Si la primera columna de la lista de argumentos de una instrucción CREATE TABLE crea un índice, no se puede incluir una segunda columna en la lista de argumentos.  
  
 Por ejemplo, para utilizar las columnas de número de pedido de cliente y número de línea como índice único en la tabla SO_LINES, utilice la instrucción:  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 Para utilizar la columna de número de pieza como un índice no único en la tabla SO_LINES, utilice la instrucción:  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 Tenga en cuenta que cuando se realizan dos instrucciones CREATE INDEX, la primera instrucción siempre creará un índice principal con el mismo nombre que la tabla y la segunda instrucción siempre creará un índice no único con el mismo nombre que la columna. Estos índices se denominarán de esta manera incluso si se introducen nombres diferentes en las instrucciones CREATE INDEX e incluso si el índice se etiqueta UNIQUE en la segunda instrucción CREATE INDEX.  
  
> [!NOTE]  
>  Cuando se utiliza el controlador Paradox sin implementar El motor de base de datos de Borland, solo se permiten instrucciones de lectura y anexar.

---
title: CREAR el índice de Paradox | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 15e16fb311bf3c9acb2823772247e0fc16eabeef
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649053"
---
# <a name="create-index-for-paradox"></a>CREAR el índice de Paradox
La sintaxis de la instrucción CREATE INDEX para el controlador de Paradox ODBC es:  
  
 **CREAR** [**UNIQUE**] **índice** *nombre de índice*  
  
 **ON** *nombre de tabla*  
  
 **(** *identificador de columna* [**ASC**]  
  
 [**,** *identificador de columna* [**ASC**]...] **)**  
  
 El controlador de Paradox ODBC no admite la **DESC** palabra clave en la gramática de SQL de ODBC para la instrucción CREATE INDEX. El *nombre-tabla* argumento puede especificar la ruta de acceso completa de la tabla.  
  
 Si la palabra clave **UNIQUE** se especifica, el controlador ODBC Paradox creará un índice único. El primer índice único se crea como un índice principal. Se trata de un archivo de clave de Paradox principal denominado *nombre-tabla*. PX. Índices principales son las siguientes restricciones:  
  
-   El índice principal debe crearse antes de que todas las filas se agregan a la tabla.  
  
-   En las primeras columnas de "n" en una tabla, se debe definir un índice principal.  
  
-   Se permite un solo índice principal por tabla.  
  
-   Una tabla no se puede actualizar el controlador de Paradox si un índice principal no está definido en la tabla. (Tenga en cuenta que esto no es cierto para una tabla vacía, que se puede actualizar incluso si no está definido un índice único en la tabla.)  
  
-   El *nombre del índice* argumento para un índice principal debe ser el mismo que el nombre de base de la tabla, según sea necesario Paradox.  
  
 Si la palabra clave **UNIQUE** es se omite, el controlador de Paradox ODBC creará un índice no único. Esto consta de dos archivos de índice secundario de Paradox denominados *nombre-tabla*. X*nn* y *nombre-tabla*. Y*nn*, donde *nn* es el número de la columna en la tabla. Índices no únicos están sujetos a las restricciones siguientes:  
  
-   Antes de poder crear un índice no único para una tabla, debe existir un índice principal de esa tabla.  
  
-   Para Paradox 3. *x*, *nombre del índice* argumento para todos los índices que no sea un índice principal (que no es único o) debe ser el mismo que el nombre de columna. Para Paradox 4. *x* y 5. *x*, puede ser el nombre de ese índice, pero no tiene que ser el mismo que el nombre de columna.  
  
-   Puede especificarse una única columna para un índice no único.  
  
 No se puede agregar columnas una vez que se ha definido un índice en una tabla. Si la primera columna de la lista de argumentos de una instrucción CREATE TABLE crea un índice, una segunda columna no puede incluirse en la lista de argumentos.  
  
 Por ejemplo, para usar el número de pedido de ventas y las columnas numéricas de línea como el índice único en la tabla SO_LINES, use la instrucción:  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 Para usar la columna de número de parte como un índice no único en la tabla SO_LINES, use la instrucción:  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 Tenga en cuenta que cuando se realizan dos instrucciones CREATE INDEX, la primera instrucción siempre creará un índice principal con el mismo nombre que la tabla y la segunda instrucción siempre creará un índice no único con el mismo nombre que la columna. Estos índices se denominará así incluso si se especifican nombres diferentes en las instrucciones CREATE INDEX e incluso si el índice está etiquetado UNIQUE en la segunda instrucción CREATE INDEX.  
  
> [!NOTE]  
>  Cuando utilice el controlador de Paradox sin necesidad de implementar el motor de base de datos de Borland, solo lectura y en anexos se permiten las instrucciones.

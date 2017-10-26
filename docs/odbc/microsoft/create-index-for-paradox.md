---
title: "Crear índice para Paradox | Documentos de Microsoft"
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
- CREATE INDEX [ODBC]
- Paradox driver [ODBC], create index
ms.assetid: 6472bd69-b931-4bc2-a9bf-f1873ed4cdfe
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 058677892aa1a3266b1cd93a5ff015ed0a14bcb9
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="create-index-for-paradox"></a>CREAR el índice de Paradox
La sintaxis de la instrucción CREATE INDEX para el controlador de ODBC Paradox es:  
  
 **CREAR** [**UNIQUE**] **índice** *nombre de índice*  
  
 **ON** *nombre de la tabla*  
  
 **(** *identificador de la columna* [**ASC**]  
  
 [**,** *identificador de la columna* [**ASC**]...] **)**  
  
 El controlador ODBC Paradox no admite la **DESC** palabra clave en la gramática de SQL de ODBC para la instrucción CREATE INDEX. El *nombre de la tabla* argumento puede especificar la ruta de acceso completa de la tabla.  
  
 Si la palabra clave **UNIQUE** se especifica, el controlador ODBC Paradox creará un índice único. El primer índice único se crea como un índice principal. Se trata de un archivo de clave de Paradox principal denominado *nombre de la tabla*. PX. Índices principales están sujetos a las restricciones siguientes:  
  
-   El índice principal debe crearse antes de que todas las filas se agregan a la tabla.  
  
-   En las primeras columnas de "n" en una tabla, se debe definir un índice principal.  
  
-   Se permite un único índice principal por tabla.  
  
-   Una tabla no se puede actualizar el controlador de Paradox si un índice principal no está definido en la tabla. (Tenga en cuenta que esto no es cierto para una tabla vacía, que puede actualizarse incluso si no se define un índice único en la tabla.)  
  
-   El *nombre del índice* argumento para un índice principal debe ser el mismo que el nombre de base de la tabla, según sea necesario por Paradox.  
  
 Si la palabra clave **UNIQUE** es se omite, el controlador ODBC Paradox creará un índice no único. Esto consta de dos archivos de índice secundario de Paradox denominados *nombre de la tabla*. X* nn * y *nombre de la tabla*. Y*nn*, donde * nn * es el número de la columna en la tabla. Índices no únicos están sujetos a las restricciones siguientes:  
  
-   Para poder crear un índice no único para una tabla, debe existir un índice principal para esa tabla.  
  
-   Para Paradox 3. *x*, *nombre del índice* argumento para todos los índices que no sea un índice principal (único o no es único) debe ser el mismo que el nombre de columna. Para Paradox 4. *x* y 5.* x*, puede ser el nombre de ese índice, pero no tiene que ser el mismo que el nombre de columna.  
  
-   Solo una columna se puede especificar para un índice no único.  
  
 No se pueden agregar columnas una vez que se ha definido un índice en una tabla. Si la primera columna de la lista de argumentos de una instrucción CREATE TABLE crea un índice, una segunda columna no puede incluirse en la lista de argumentos.  
  
 Por ejemplo, para utilizar el número de pedido de ventas y línea de las columnas numéricas como el índice único en la tabla SO_LINES, use la instrucción:  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 Para usar la columna de número de elemento como un índice no único en la tabla SO_LINES, use la instrucción:  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 Tenga en cuenta que cuando se realizan dos instrucciones CREATE INDEX, la primera instrucción siempre creará un índice principal con el mismo nombre que la tabla y la segunda instrucción siempre creará un índice no único con el mismo nombre que la columna. Estos índices se denominará así incluso si se especifican nombres diferentes en las instrucciones CREATE INDEX e incluso si el índice es UNIQUE en la segunda instrucción CREATE INDEX.  
  
> [!NOTE]  
>  Cuando se utiliza el controlador de Paradox sin necesidad de implementar el motor de base de datos de Borland, solo lectura y anexar se permiten las instrucciones.


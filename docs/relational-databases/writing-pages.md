---
description: Escribir páginas
title: Escribir páginas | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- pages
ms.assetid: 409c8753-03c4-436d-839c-6a5879971551
author: pmasl
ms.author: pelopes
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3c9fc200c47ffdb82c15a86469244cd17bd75821
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97403396"
---
# <a name="writing-pages"></a>Escribir páginas
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

La E/S de una instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)] incluye escrituras lógicas y físicas. Se produce una escritura lógica cuando se modifican los datos en una página de la caché del búfer. Una escritura física se produce cuando la página se escribe de la [caché del búfer](../relational-databases/memory-management-architecture-guide.md) al disco.

Cuando se modifica una página en la caché del búfer, no se vuelve a escribir inmediatamente en el disco; en su lugar, la página se marca como desfasada. Significa que una página puede tener más de una escritura lógica antes de que se escriba físicamente en el disco. Para cada escritura lógica, se inserta una entrada del registro de transacciones en la caché del registro que registra la modificación. Las entradas del registro se tienen que escribir en el disco antes de que la página desfasada asociada se quite de la caché del búfer y se escriba en el disco. SQL Server usa una técnica conocida como registro de escritura anticipada que impide escribir una página desfasada antes de que el registro asociado se escriba en el disco. Esto es fundamental para el funcionamiento correcto del administrador de recuperaciones. Para más información, consulte [Registro de transacciones de escritura anticipada](../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md).

La siguiente ilustración muestra el proceso de escritura de una página de datos modificada.

![Writing_Pages](../relational-databases/media/writing-pages.gif)

Cuando el administrador del búfer escribe una página, busca páginas desfasadas adyacentes que puedan incluirse en una sola operación de recopilación y escritura. Las páginas adyacentes tienen Id. de página consecutivos y son del mismo archivo; las páginas no tienen que ser contiguas en la memoria. La búsqueda continúa hacia delante y hacia atrás hasta que se produce uno de los siguientes eventos:

 * Se encuentra una página limpia.
 * Se encuentran 32 páginas.
 * Se encuentra una página desfasada cuyo número de secuencia de registro (LSN) aún no se ha vaciado en el registro.
 * Se encuentra una página a la que no se le puede establecer un bloqueo temporal inmediatamente.

De este modo, todo el conjunto de páginas se puede escribir en el disco con una sola operación de recopilación y escritura. 

Justo antes de que se escriba una página, la forma de protección de página especificada en la base de datos se agrega a la página. Si se agrega la protección contra página rasgada, se debe establecer un bloqueo temporal en la página EX(clusivamente) para la E/S. Esto se debe a que la protección contra página rasgada modifica la página y no se puede leer ningún otro subproceso. Si se agrega protección de suma de comprobación de página o la base de datos no usa protección de página, se establece un bloqueo temporal UP (actualización) para la E/S en la página. Este bloqueo temporal evita que nadie modifique la página durante la escritura, pero permite a los lectores usarla. Para más información sobre las opciones de protección de página de E/S de disco, consulte [Administración de búfer](../relational-databases/memory-management-architecture-guide.md).

Una página desfasada se escribe en el disco de una de estas tres maneras: 

* Escritura diferida   
 La escritura diferida es un proceso del sistema que mantiene tres búferes disponibles quitando las páginas usadas con poca frecuencia de la caché del búfer. Las páginas desfasadas se escriben en primer lugar en el disco. 

* Escritura ///diligente///   
 El proceso de escritura diligente escribe páginas desfasadas de datos asociadas a operaciones con registro mínimo, como BULK INSERT y SELECT INTO. Este proceso permite que la creación y escritura de nuevas páginas tengan lugar en paralelo. Es decir, la operación de llamada no tiene que esperar hasta que termine toda la operación antes de escribir las páginas en el disco.

* Punto de control   
 El proceso de punto de comprobación examina periódicamente la caché del búfer en busca de búferes con páginas de una base de datos especificada y escribe todas las páginas desfasadas en el disco. Los puntos de comprobación permiten ahorrar tiempo en una recuperación posterior al crear un punto en el que se garantiza que todas las páginas desfasadas se hayan escrito en el disco. El usuario puede solicitar una operación de punto de comprobación mediante el comando CHECKPOINT o [!INCLUDE[ssDE](../includes/ssde-md.md)] puede generar puntos de comprobación automáticos que se basen en la cantidad de espacio de registro utilizado y el tiempo transcurrido desde el último punto de comprobación. Además, se genera un punto de comprobación cuando se producen determinadas actividades. Por ejemplo, cuando se agrega o quita un archivo de datos o de registro de una base de datos, o cuando se detiene la instancia de SQL Server. Para más información, consulte [Puntos de comprobación y la parte activa del registro](../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md).

Los procesos de escritura diferida, escritura ///diligente/// y punto de comprobación no esperan a que se complete la operación de E/S. Siempre usan la operación de E/S asincrónica (o superpuesta) y continúan con otros trabajos; posteriormente, comprueban que la operación de E/S sea correcta. De este modo, SQL Server maximiza los recursos de la CPU y de E/S para las tareas apropiadas.

## <a name="see-also"></a>Consulte también
[Guía de arquitectura de páginas y extensiones](../relational-databases/pages-and-extents-architecture-guide.md)   
 [Leer páginas](../relational-databases/reading-pages.md)

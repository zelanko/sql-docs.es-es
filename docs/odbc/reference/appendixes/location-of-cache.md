---
title: Ubicación de la caché ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 240d6162-4da6-4b1f-96c7-f379f4ecb16f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 13510332ae8bfab07a13d7831f9f74a048551214
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288623"
---
# <a name="location-of-cache"></a>Ubicación de caché
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 La biblioteca de cursores almacena en caché los datos en la memoria y en Windows® archivos temporales. Esto limita el tamaño del conjunto de resultados que la biblioteca de cursores puede controlar solo por el espacio en disco disponible. Se utiliza un archivo temporal cuando los datos que se van a almacenar en caché cruzarían el límite del segmento si se insertan al final de la caché de la biblioteca de cursores. En su lugar, los datos que se van a almacenar en caché se agregan en lugar del último bloque de datos guardado en la memoria caché. El último bloque de datos guardado se guarda en un archivo temporal. Si la biblioteca de cursores finaliza de forma anormal, como cuando se produce un error en la alimentación, puede dejar archivos temporales de Windows en el disco. Estos se denominan .ctT*nnnn*.tmp y se crean en el directorio actual.  
  
> [!NOTE]  
>  Si la biblioteca de cursores de Microsoft® WindowsNT®/Windows2000 intenta almacenar en caché los datos de un archivo temporal en el directorio actual mientras la aplicación se ejecuta desde un recurso compartido de solo lectura o un disco compacto (como un ejemplo de biblioteca de clases de Microsoft Foundation), se devolverá SQLSTATE HY000 (Error general que no puede crear un búfer de archivos).

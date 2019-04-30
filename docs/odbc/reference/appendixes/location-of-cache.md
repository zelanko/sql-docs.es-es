---
title: Ubicación de caché | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b1ffd8c56a6727a892cb518222c961bbb6c794c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181348"
---
# <a name="location-of-cache"></a>Ubicación de caché
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 La biblioteca de cursores se almacena en caché datos en memoria y en los archivos temporales de Windows®. Esto limita el tamaño del conjunto de resultados que puede administrar la biblioteca de cursores solo por espacio en disco disponible. Un archivo temporal se usa cuando los datos en la memoria caché crucen el límite de segmento si se insertan al final de la caché de la biblioteca de cursores. En su lugar, se agregan los datos que se va a almacenar en caché en lugar de la última bloque de datos en la memoria caché. Guardado por el último bloque de datos se guarda en un archivo temporal. Si la biblioteca de cursores se finaliza correctamente, por ejemplo, cuando se produce un error en la eficacia, puede dejar los archivos temporales de Windows en el disco. Se denominan ~ CTT*nnnn*.tmp y se crean en el directorio actual.  
  
> [!NOTE]  
>  Si la biblioteca de cursores en Microsoft® WindowsNT®/Windows 2000 intenta almacenar datos en caché en un archivo temporal en el directorio actual mientras se ejecuta la aplicación desde un recurso compartido de solo lectura o un disco compacto (por ejemplo, un ejemplo de biblioteca Microsoft Foundation Class), SQLSTATE HY000 (General Error-Unable crear un búfer de archivo) se devolverá.

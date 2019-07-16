---
title: Procesamiento de instrucciones SELECT FOR UPDATE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], select for update statements
- select for update [ODBC]
- SQL statements [ODBC], cursor library
- cursor library [ODBC], select for update statements
- ODBC cursor library [ODBC], select for update statements
- cursor library [ODBC], statement processing
ms.assetid: 8d2e79a4-5daf-458e-a536-d8b6e588753e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8ad9a20ab8abd40123ec4e4d7369373e68699205
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028359"
---
# <a name="processing-select-for-update-statements"></a>Procesamiento de instrucciones SELECT FOR UPDATE
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Para obtener la máxima interoperatividad, las aplicaciones deben generar conjuntos de resultados que se actualizará con una instrucción de actualización posicionada mediante la ejecución de un **seleccione para actualizar** instrucción. Aunque la biblioteca de cursores no requiere esto, es necesaria para la mayoría de los orígenes de datos que admiten las instrucciones update posicionadas.  
  
 La biblioteca de cursores pasa por alto las columnas de la **FOR UPDATE** cláusula de una **SELECT FOR UPDATE** instrucción; quita esta cláusula antes de pasar la instrucción del controlador. En la biblioteca de cursores, el atributo de instrucción SQL_ATTR_CONCURRENCY, junto con las restricciones mencionadas en la sección anterior, los controles si establecen las columnas de un resultado se pueden actualizar.

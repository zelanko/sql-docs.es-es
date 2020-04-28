---
title: Procesando SELECT para instrucciones UPDATE | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 904028cd7b3798fcac8f9e5afa6186fae3e9fa29
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81308016"
---
# <a name="processing-select-for-update-statements"></a>Procesamiento de instrucciones SELECT FOR UPDATE
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en los nuevos trabajos de desarrollo y planee modificar las aplicaciones que actualmente la utilizan. Microsoft recomienda el uso de la funcionalidad de cursor del controlador.  
  
 Para obtener la máxima interoperabilidad, las aplicaciones deben generar conjuntos de resultados que se actualizarán con una instrucción UPDATE posicionada mediante la ejecución de una instrucción **Select for update** . Aunque la biblioteca de cursores no lo requiere, la mayoría de los orígenes de datos que admiten instrucciones Update posicionadas lo requieren.  
  
 La biblioteca de cursores omite las columnas de la cláusula **for update** de una instrucción **Select for update** . quita esta cláusula antes de pasar la instrucción al controlador. En la biblioteca de cursores, el atributo de instrucción SQL_ATTR_CONCURRENCY, junto con las restricciones mencionadas en la sección anterior, controla si se pueden actualizar las columnas de un conjunto de resultados.

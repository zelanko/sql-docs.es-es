---
title: Procesamiento de SELECT PARA Las instrucciones DE ACTUALIZACIÓN ? Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81308016"
---
# <a name="processing-select-for-update-statements"></a>Procesamiento de instrucciones SELECT FOR UPDATE
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 Para obtener la máxima interoperabilidad, las aplicaciones deben generar conjuntos de resultados que se actualizarán con una instrucción update posicionada ejecutando una instrucción **SELECT FOR UPDATE.** Aunque la biblioteca de cursores no requiere esto, la mayoría de los orígenes de datos que admiten instrucciones de actualización posicionadas lo requieren.  
  
 La biblioteca de cursores omite las columnas de la cláusula **FOR UPDATE** de una instrucción SELECT **FOR UPDATE;** quita esta cláusula antes de pasar la instrucción al controlador. En la biblioteca de cursores, el atributo de instrucción SQL_ATTR_CONCURRENCY, junto con las restricciones mencionadas en la sección anterior, controla si las columnas de un conjunto de resultados se pueden actualizar.

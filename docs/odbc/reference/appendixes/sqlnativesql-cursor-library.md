---
title: SQLNativeSql (Biblioteca de cursores) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLNativeSql function [ODBC], Cursor Library
ms.assetid: c4459092-1177-4b2a-b7f5-e0083d3bf2b2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 41f7617530f34d49852ca67db9f47cab94292385
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300575"
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLNativeSql** en la biblioteca de cursores. Para obtener información general acerca de **SQLNativeSql**, vea [SQLNativeSql Function](../../../odbc/reference/syntax/sqlnativesql-function.md).  
  
 Si el controlador admite esta función, la biblioteca de cursores llama a **SQLNativeSql** en el controlador y le pasa la instrucción SQL. Para las instrucciones de actualización posicionada, eliminación posicionada y **SELECT FOR UPDATE,** la biblioteca de cursores modifica la instrucción antes de pasarla al controlador.  
  
> [!NOTE]  
>  La biblioteca de cursores devuelve incorrectamente SQLSTATE 34000 (nombre del cursor no válido) si el nombre del cursor no es válido en una instrucción de actualización o eliminación posicionada que se pasa en el argumento *InStatementText* de **SQLNativeSql**. **SQLNativeSql** no está pensado para devolver errores de sintaxis, que se devuelven solo en la preparación o ejecución de la instrucción.

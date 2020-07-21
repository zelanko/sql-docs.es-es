---
title: SQLSetEnvAttr y la biblioteca de cursores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC], Cursor Library
ms.assetid: 59cc8eae-09ae-4796-869a-c5806488ae83
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 42d6804bf8a3544de44c03266ce28712e1b04d90
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300525"
---
# <a name="sqlsetenvattr-and-the-cursor-library"></a>SQLSetEnvAttr y la biblioteca de cursores
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en los nuevos trabajos de desarrollo y planee modificar las aplicaciones que actualmente la utilizan. Microsoft recomienda el uso de la funcionalidad de cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLSetEnvAttr** con la biblioteca de cursores. Para obtener información general sobre **SQLSetEnvAttr**, consulte la [función SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
 La biblioteca de cursores no se ve afectada por la configuración del atributo de entorno SQL_ATTR_ODBC_VERSION, independientemente de la versión de la aplicación o de la versión del controlador.

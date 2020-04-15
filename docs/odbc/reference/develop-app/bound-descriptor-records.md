---
title: Registros de descriptores enlazados (Bound Descriptor Records) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 155ef4951abddc7a73d9d4abfbc45248f33d653c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306312"
---
# <a name="bound-descriptor-records"></a>Registros de Descriptor de enlace
Cuando la aplicación establece el campo SQL_DESC_DATA_PTR de un registro descriptor para que ya no contenga un valor nulo, se dice que el registro está *enlazado.*  
  
 Si el descriptor es un APD, cada registro enlazado constituye un parámetro enlazado. Para los parámetros de entrada, la aplicación debe enlazar un parámetro para cada marcador de parámetro dinámico en la instrucción SQL antes de ejecutar la instrucción. Para los parámetros de salida, la aplicación no necesita enlazar el parámetro.  
  
 Si el descriptor es un ARD, que describe una fila de datos de base de datos, cada registro enlazado constituye una columna enlazada.

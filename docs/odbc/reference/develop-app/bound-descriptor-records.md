---
description: Registros de Descriptor de enlace
title: Registros de descriptor enlazado | Microsoft Docs
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
ms.openlocfilehash: fcf88374967b5a9d8426d16c9e92c06e4eef32cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476807"
---
# <a name="bound-descriptor-records"></a>Registros de Descriptor de enlace
Cuando la aplicación establece el campo de SQL_DESC_DATA_PTR de un registro de descriptor para que ya no contenga un valor null, se dice que el registro está *enlazado*.  
  
 Si el descriptor es un APD, cada registro enlazado constituye un parámetro enlazado. En el caso de los parámetros de entrada, la aplicación debe enlazar un parámetro para cada marcador de parámetro dinámico en la instrucción SQL antes de ejecutar la instrucción. En el caso de los parámetros de salida, la aplicación no necesita enlazar el parámetro.  
  
 Si el descriptor es un ARD, que describe una fila de datos de la base de datos, cada registro enlazado constituye una columna enlazada.

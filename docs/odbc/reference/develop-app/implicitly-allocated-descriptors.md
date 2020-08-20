---
description: Descriptores implícitamente asignados
title: Descriptores asignados implícitamente | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- implicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 9f88c863-affc-4ab4-a558-63a3ef766f37
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5daa7f622798e1394c186b333069933b48e367af
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461427"
---
# <a name="implicitly-allocated-descriptors"></a>Descriptores implícitamente asignados
Cuando se asigna un identificador de instrucción, la aplicación asigna implícitamente un conjunto de cuatro descriptores. La aplicación puede obtener los identificadores de estos descriptores asignados implícitamente como atributos del identificador de instrucción. Cuando la aplicación libera el identificador de instrucción, el controlador libera todos los descriptores asignados implícitamente en ese controlador.

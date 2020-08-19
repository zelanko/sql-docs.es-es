---
description: Cargar por ordinal
title: Cargando por ordinal | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], loading by ordinal
- compatibility [ODBC], loading by ordinal
- loading by ordinal [ODBC]
ms.assetid: 337d90ab-68eb-4940-a2f3-f7d5693ee766
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb8929962e97e7560f50117218f621cd21846fc4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429637"
---
# <a name="loading-by-ordinal"></a>Cargar por ordinal
En ODBC *2. x*, se puede realizar la carga por ordinal para mejorar el rendimiento del proceso de conexión. Un controlador ODBC *2. x* exporta una función ficticia con el ordinal 199; Cuando el administrador de controladores lo detecta, resuelve las direcciones de las funciones ODBC por ordinal, no por nombre. Esta funcionalidad todavía se admite para los controladores ODBC *2. x* , pero no se admite para los controladores ODBC *3. x* .

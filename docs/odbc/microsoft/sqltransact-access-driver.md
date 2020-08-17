---
description: SQLTransact (controlador de Access)
title: SQLTransact (controlador de Access) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLTransact
- SQLTransact function [ODBC], Access Driver
ms.assetid: 892b79c7-9e20-4d1f-bc60-d4b25694ca25
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e9b00f8f5a12af2d3823171d22ad53106569352
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339707"
---
# <a name="sqltransact-access-driver"></a>SQLTransact (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Cuando se usa el controlador de Microsoft Access, se admiten SQL_COMMIT y SQL_ROLLBACK para el argumento *fType* en una llamada a **SQLTransact**.  
  
 Si se produce un error durante el proceso de confirmación, la base de datos afectada se puede reparar mediante la opción reparar base de datos del programa de instalación del controlador de Microsoft Access o mediante el uso de la palabra clave REPAIR_DB en la función **SQLConfigDataSource** .

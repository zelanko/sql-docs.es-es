---
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
ms.openlocfilehash: 4f88d3154925ab589a8519cb9205da03e8c3dc08
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299274"
---
# <a name="sqltransact-access-driver"></a>SQLTransact (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Cuando se usa el controlador de Microsoft Access, se admiten SQL_COMMIT y SQL_ROLLBACK para el argumento *fType* en una llamada a **SQLTransact**.  
  
 Si se produce un error durante el proceso de confirmación, la base de datos afectada se puede reparar mediante la opción reparar base de datos del programa de instalación del controlador de Microsoft Access o mediante el uso de la palabra clave REPAIR_DB en la función **SQLConfigDataSource** .

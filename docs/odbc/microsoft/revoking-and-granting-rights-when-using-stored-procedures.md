---
description: Revocación y conceder derechos al usar procedimientos almacenados
title: Revocar y conceder derechos al usar procedimientos almacenados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 24070039-03ab-4623-a681-6308802eb399
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ad59f18f040dd1fefec606c99e3cce5f1002c22a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449277"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>Revocación y conceder derechos al usar procedimientos almacenados
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC de Microsoft para Oracle devuelve el siguiente mensaje de error cuando se conceden derechos de usuario y, a continuación, se revocan en una tabla a la que se obtiene acceso mediante un procedimiento almacenado:  
  
 SQL_ERROR =-1  
  
 szErrorMsg = "[Microsoft] [controlador ODBC para Oracle] número incorrecto de parámetros"  
  
 szErrorMsg = "[Microsoft] [controlador ODBC para Oracle] error de sintaxis o infracción de acceso"  
  
 En este escenario, se produce un error en la llamada a la función OCI de Oracle Odessp (), pero es necesario para implementar parámetros predeterminados. Una vez que se modifican los permisos de la tabla subyacente, el procedimiento almacenado se debe volver a compilar antes de ejecutarlo de nuevo.

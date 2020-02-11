---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 91fcf722554fe1840465329e707c792a6bbab6db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67987955"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>Revocación y conceder derechos al usar procedimientos almacenados
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC de Microsoft para Oracle devuelve el siguiente mensaje de error cuando se conceden derechos de usuario y, a continuación, se revocan en una tabla a la que se obtiene acceso mediante un procedimiento almacenado:  
  
 SQL_ERROR =-1  
  
 szErrorMsg = "[Microsoft] [controlador ODBC para Oracle] número incorrecto de parámetros"  
  
 szErrorMsg = "[Microsoft] [controlador ODBC para Oracle] error de sintaxis o infracción de acceso"  
  
 En este escenario, se produce un error en la llamada a la función OCI de Oracle Odessp (), pero es necesario para implementar parámetros predeterminados. Una vez que se modifican los permisos de la tabla subyacente, el procedimiento almacenado se debe volver a compilar antes de ejecutarlo de nuevo.

---
title: Almacena las limitaciones de parámetro de procedimiento | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 8b804bcf-4cce-4e6f-aa45-00bab9ef9921
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ecaf64ac29804034e47588e1686981f91a3fd16a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="stored-procedure-parameter-limitations"></a>Limitaciones de parámetro de procedimiento almacenado
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Cuando se está ejecutando Oracle procedimientos almacenados que utilizan 10 o más parámetros de salida, la llamada al procedimiento almacenado se producirá un error, lo que produce un error de infracción de acceso o ActiveX Data Objects (ADO). Esto puede ocurrir cuando se usa el controlador ODBC de Microsoft para Oracle con las versiones 8.0.4.0.0 y 8.0.4.0.4 del software de cliente de Oracle.  
  
 Para corregir el problema, el software de cliente de Oracle debe ser actualizado a la versión 8.0.4.2.0 o superior. Póngase en contacto con Oracle Corporation para obtener más información sobre la [revisiones](../../odbc/microsoft/oracle-software-patches.md).  
  
> [!NOTE]  
>  Este problema no ocurre con las primeras versiones de Oracle versión del software cliente 8.0.3.0.0.

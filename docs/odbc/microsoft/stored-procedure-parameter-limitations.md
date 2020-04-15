---
title: Limitaciones de los parámetros de procedimiento almacenados ? Microsoft Docs
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
ms.assetid: 8b804bcf-4cce-4e6f-aa45-00bab9ef9921
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbd748884575791d5f170e95bc5aa465b61624b7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299205"
---
# <a name="stored-procedure-parameter-limitations"></a>Limitaciones de parámetro de procedimiento almacenado
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Al ejecutar procedimientos almacenados de Oracle que utilizan 10 o más parámetros de salida, se producirá un error en la llamada a procedimiento almacenado, lo que provocará un error de infracción de acceso o de objetos de datos ActiveX (ADO). Esto puede ocurrir cuando se utiliza el controlador ODBC de Microsoft para Oracle con las versiones 8.0.4.0.0 y 8.0.4.0.4 del software cliente de Oracle.  
  
 Para corregir el problema, el software cliente de Oracle debe actualizarse a la versión 8.0.4.2.0 o superior. Póngase en contacto con Oracle Corporation para obtener más información sobre los [parches.](../../odbc/microsoft/oracle-software-patches.md)  
  
> [!NOTE]  
>  Este problema no se produce con la versión temprana de la versión 8.0.3.0.0 del software cliente de Oracle.

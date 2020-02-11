---
title: Limitaciones de los parámetros de procedimientos almacenados | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 36f1c5a18eb9f0b1939a2c3602f1ebe7695741f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948823"
---
# <a name="stored-procedure-parameter-limitations"></a>Limitaciones de parámetro de procedimiento almacenado
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Cuando se ejecutan procedimientos almacenados de Oracle que usan 10 o más parámetros de salida, se producirá un error en la llamada al procedimiento almacenado, lo que provocará un error de infracción de acceso o de Objetos de datos ActiveX (ADO). Esto puede ocurrir cuando se usa el controlador ODBC de Microsoft para Oracle con las versiones 8.0.4.0.0 y 8.0.4.0.4 del software cliente de Oracle.  
  
 Para corregir el problema, el software de cliente de Oracle debe actualizarse a la versión 8.0.4.2.0 o posterior. Póngase en contacto con Oracle Corporation para obtener más información acerca de las [revisiones](../../odbc/microsoft/oracle-software-patches.md).  
  
> [!NOTE]  
>  Este problema no se produce con la versión temprana de la versión 8.0.3.0.0 del software cliente de Oracle.

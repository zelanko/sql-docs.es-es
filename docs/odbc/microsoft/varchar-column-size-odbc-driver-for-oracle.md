---
title: Tamaño de la columna VARCHAR (controlador ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- varchar column size [ODBC]
- ODBC driver for Oracle [ODBC], data types
ms.assetid: eb4cb410-3d00-4251-8c5e-a06f36c4dac7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3a3156c3f71eb4b3f7b8319da5d5fec7514f08b6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087966"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>Tamaño de la columna VARCHAR (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 En Oracle8, el tamaño máximo de una columna VARCHAR ha aumentado de 2000 a 4000 bytes. El software cliente de Oracle 7.3. x no tiene forma de enlazar un valor de parámetro de más de 2000 bytes. Por lo tanto, si crea una tabla con una columna VARCHAR de más de 2000 bytes, no podrá realizar inserciones, actualizaciones, eliminaciones y consultas parametrizadas con datos que superen el límite de 2000 bytes del software cliente. Dado que el controlador ODBC para Oracle y el proveedor de OLE DB para Oracle usan inserciones, actualizaciones, eliminaciones y consultas con parámetros, se notificarán errores ORA-01026 en este caso. Los datos que se encuentran dentro de los límites exigidos por el software de cliente de Oracle funcionarán. Para evitar este límite de 2000 bytes, debe actualizar el software cliente a Oracle8 (8.0.4.1.1 c o posterior).

---
title: Tamaño de la columna VARCHAR (controlador ODBC para Oracle) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f11e1de3171521c57c80beb207d33e67d26d3e33
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304830"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>Tamaño de la columna VARCHAR (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 En Oracle8, el tamaño máximo de una columna VARCHAR ha aumentado de 2000 a 4000 bytes. El software cliente Oracle 7.3.x no tiene forma de enlazar un valor de parámetro superior a 2000 bytes. Por lo tanto, si crea una tabla con una columna VARCHAR de más de 2000 bytes, no podrá realizar inserciones, actualizaciones, eliminaciones y consultas parametrizadas en ella con datos que superen el límite de 2000 bytes del software cliente. Dado que tanto el controlador ODBC para Oracle como el proveedor OLE DB para Oracle usan inserciones, actualizaciones, eliminaciones y consultas parametrizadas, notificarán errores ORA-01026 en este caso. Los datos que se encuentran dentro de los límites aplicados por el software cliente de Oracle funcionarán. Para evitar este límite de 2000 bytes, debe actualizar el software cliente a Oracle8 (8.0.4.1.1c o superior).

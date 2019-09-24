---
title: Subclave de orígenes de datos ODBC | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], for data sources
- data sources [ODBC], subkeys
- registry entries for data sources [ODBC], subkeys
ms.assetid: 0a8ccb80-c573-4418-84e5-f04a2b0e2ac1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4d6d54d1fc7c7742bf94e91d7370f356e28b5624
ms.sourcegitcommit: 816ff47eeab157c66e0f75f18897a63dc8033502
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71207687"
---
# <a name="odbc-data-sources-subkey"></a>Subclave de orígenes de datos ODBC

Los valores de la `ODBC Data Sources` subclave enumeran los orígenes de datos. El formato de estos valores se muestra en la tabla siguiente.

| NOMBRE | Tipo de datos | Datos |
| :--- | :-------- | :--- |
| *data-source-name* | REG_SZ | *driver-description* |
| &nbsp; | &nbsp; | &nbsp; |

El valor del *nombre del origen de datos* se define mediante el programa de administración (que normalmente solicita el usuario) y el desarrollador del controlador define la descripción del *controlador* (normalmente es el nombre del DBMS asociado con el controlador).

Por ejemplo, supongamos que se han definido tres orígenes de datos: Inventario, que utiliza SQL Server; Payroll, que utiliza dBASE; y personal, que utiliza archivos de texto con formato. Los valores de la `ODBC Data Sources` subclave pueden ser los siguientes:

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```

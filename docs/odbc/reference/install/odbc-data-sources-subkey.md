---
description: Subclave de orígenes de datos ODBC
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9897c68d110f59d03ac8e1b3e403ed21844082fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448937"
---
# <a name="odbc-data-sources-subkey"></a>Subclave de orígenes de datos ODBC

Los valores de la `ODBC Data Sources` subclave enumeran los orígenes de datos. El formato de estos valores se muestra en la tabla siguiente.

| Nombre | Tipo de datos | data |
| :--- | :-------- | :--- |
| *nombre del origen de datos* | REG_SZ | *controlador: Descripción* |
| &nbsp; | &nbsp; | &nbsp; |

El valor del *nombre del origen de datos* se define mediante el programa de administración (que normalmente solicita el usuario) y el desarrollador del controlador define la descripción del *controlador* (normalmente es el nombre del DBMS asociado con el controlador).

Por ejemplo, supongamos que se han definido tres orígenes de datos: Inventory, que utiliza SQL Server; Payroll, que utiliza dBASE; y personal, que utiliza archivos de texto con formato. Los valores de la `ODBC Data Sources` subclave pueden ser los siguientes:

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```

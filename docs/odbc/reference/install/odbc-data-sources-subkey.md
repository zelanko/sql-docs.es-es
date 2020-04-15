---
title: Subclave Orígenes de datos ODBC (ODBC Data Sources) Microsoft Docs
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
ms.openlocfilehash: c5e97e643a78187b15e91833c832cd16ca435c7f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304066"
---
# <a name="odbc-data-sources-subkey"></a>Subclave Orígenes de datos ODBC

Los valores `ODBC Data Sources` de la subclave enumeran los orígenes de datos. El formato de estos valores se muestra en la tabla siguiente.

| Nombre | Tipo de datos | data |
| :--- | :-------- | :--- |
| *nombre-fuente de datos* | REG_SZ | *descripción del conductor* |
| &nbsp; | &nbsp; | &nbsp; |

El programa de administración define el valor *data-source-name* (que normalmente solicita al usuario) y el desarrollador del controlador define *la descripción del controlador* (normalmente es el nombre del DBMS asociado al controlador).

Por ejemplo, supongamos que se han definido tres orígenes de datos: Inventario, que usa SQL Server; Nómina, que utiliza dBASE; y Personal, que utiliza archivos de texto con formato. Los valores `ODBC Data Sources` de la subclave pueden ser los siguientes:

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```

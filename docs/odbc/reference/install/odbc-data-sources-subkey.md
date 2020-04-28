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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c5e97e643a78187b15e91833c832cd16ca435c7f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304066"
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

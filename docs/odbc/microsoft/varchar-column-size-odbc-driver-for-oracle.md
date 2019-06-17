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
manager: craigg
ms.openlocfilehash: db2871324f92ef6d84a8bf8313db105489100a96
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232159"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>Tamaño de la columna VARCHAR (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 En Oracle8, ha aumentado el tamaño máximo de una columna VARCHAR de 2000 a 4.000 bytes. El software de cliente de Oracle 7.3.x no tiene ninguna manera de enlazar un valor de parámetro más de 2000 bytes. Por lo tanto, si crea una tabla con una columna VARCHAR de más de 2000 bytes, podrá realizar con parámetros inserciones, actualizaciones, eliminaciones y consultas con él con datos que superan el límite de 2000 bytes del software cliente. Dado que tanto el controlador ODBC para Oracle y el proveedor OLE DB para Oracle se usan las consultas, actualizaciones, eliminaciones e inserciones con parámetros, va a notificar errores ORA-01026 en este caso. Datos que están dentro de los límites aplicados por el software cliente de Oracle funcionará. Para evitar este límite de 2000 bytes, debe actualizar el software cliente a Oracle8 (8.0.4.1.1c o superior).

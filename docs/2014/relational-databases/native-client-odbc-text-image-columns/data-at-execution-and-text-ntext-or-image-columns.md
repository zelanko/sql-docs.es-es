---
title: Datos en ejecución y Text, ntext o Image Columns | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- data-at-execution
- ODBC data-at-execution
- image columns [ODBC]
ms.assetid: 67ffb1a6-f38d-4712-ba64-96bdd41ec2b2
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d0e03c12fe94755e42c5838a66c85242cae59a62
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37416254"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>Datos en ejecución y columnas de tipo text, ntext o image
  Datos en ejecución de ODBC es una característica que habilita a las aplicaciones para trabajar con grandes volúmenes de datos en columnas o parámetros enlazados. Cuando se recuperan un gran **texto**, **ntext**, o **imagen** columnas, una aplicación no puede simplemente asignar un búfer enorme, enlazar la columna en el búfer y capturar la fila. Al actualizar un gran **texto**, **ntext**, o **imagen** columnas, la aplicación podría no poder simplemente asignar un búfer enorme, enlazarlo a un marcador de parámetro en una instancia de SQL instrucción y, a continuación, ejecute la instrucción. En estos casos, la aplicación debe utilizar [SQLGetData](../native-client-odbc-api/sqlgetdata.md) o [SQLPutData](../native-client-odbc-api/sqlputdata.md) con sus opciones de datos en ejecución.  
  
## <a name="see-also"></a>Vea también  
 [Administrar columnas de texto e imagen](managing-text-and-image-columns.md)  
  
  

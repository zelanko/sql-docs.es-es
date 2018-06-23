---
title: Datos en ejecución y Text, ntext o Image Columns | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 90777c1f7f1ac50266eaf7fe473c5ca3b1c2f189
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198892"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>Datos en ejecución y columnas de tipo text, ntext o image
  Datos en ejecución de ODBC es una característica que habilita a las aplicaciones para trabajar con grandes volúmenes de datos en columnas o parámetros enlazados. Cuando se recuperan un gran **texto**, **ntext**, o **imagen** de las columnas, una aplicación no puede ser puede simplemente asignar un búfer enorme, enlazar la columna en el búfer y capturar la fila. Cuando se actualiza un gran **texto**, **ntext**, o **imagen** columnas, la aplicación no puede simplemente asignar un búfer enorme, enlazarlo a un marcador de parámetro en un SQL instrucción y, a continuación, ejecute la instrucción. En estos casos, la aplicación debe utilizar [SQLGetData](../native-client-odbc-api/sqlgetdata.md) o [SQLPutData](../native-client-odbc-api/sqlputdata.md) con sus opciones de datos en ejecución.  
  
## <a name="see-also"></a>Vea también  
 [Administrar columnas de texto e imagen](managing-text-and-image-columns.md)  
  
  
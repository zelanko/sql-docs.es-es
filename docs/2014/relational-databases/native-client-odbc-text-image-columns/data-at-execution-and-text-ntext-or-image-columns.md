---
title: Columnas de datos en ejecución y Text, ntext o Image | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 404fade34862fe4705ec440eef7f466a9073250b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85039297"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>Datos en ejecución y columnas de tipo text, ntext o image
  Datos en ejecución de ODBC es una característica que habilita a las aplicaciones para trabajar con grandes volúmenes de datos en columnas o parámetros enlazados. Al recuperar columnas **Text**, **ntext**o **Image** muy grandes, es posible que una aplicación no pueda asignar simplemente un búfer enorme, enlazar la columna al búfer y capturar la fila. Al actualizar columnas **Text**, **ntext**o **Image** muy grandes, es posible que la aplicación no pueda asignar simplemente un búfer enorme, enlazarlo a un marcador de parámetro en una instrucción SQL y, a continuación, ejecutar la instrucción. En estos casos, la aplicación debe utilizar [SQLGetData](../native-client-odbc-api/sqlgetdata.md) o [SQLPutData](../native-client-odbc-api/sqlputdata.md) con sus opciones de datos en ejecución.  
  
## <a name="see-also"></a>Consulte también  
 [Administrar columnas de texto e imagen](managing-text-and-image-columns.md)  
  
  

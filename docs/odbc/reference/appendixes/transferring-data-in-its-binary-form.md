---
title: Transferencia de datos en su forma binaria | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], transferring in binary form
- transferring data in binary form [ODBC]
- binary data transfers [ODBC]
ms.assetid: 4b12a9de-51d0-416a-87f4-9bf84959cad9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a2897f882dc9dcd78ee8b919de01126d6be510c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070022"
---
# <a name="transferring-data-in-its-binary-form"></a>Transferencia de datos en su forma binaria
Una aplicación puede transferir con seguridad datos (en el formato interno utilizado por un DBMS especificado) entre dos orígenes de datos que usan el mismo DBMS y la plataforma de hardware. Para una parte determinada de datos, los tipos de datos SQL deben ser el mismo en los orígenes de datos de origen y de destino. El tipo de datos de C es SQL_C_BINARY.  
  
 Cuando la aplicación llama **SQLFetch**, **SQLFetchScroll**, o **SQLGetData** para recuperar los datos del origen de datos de origen, el controlador recupera los datos de los datos origen y la transfiere, sin conversión a una ubicación de almacenamiento de tipo SQL_C_BINARY. Cuando la aplicación llama **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPutData o SQLSetPos** para enviar los datos a el origen de datos de destino, el controlador recupera los datos de la ubicación de almacenamiento y la transfiere, sin la conversión, al origen de datos de destino.  
  
> [!NOTE]  
>  Las aplicaciones que transfiere datos (excepto los datos binarios) de esta manera no son interoperables entre el DBMS.  
  
 **SQLCopyDesc** puede utilizarse para copiar los enlaces de filas desde el DBMS de origen a los enlaces de parámetro en el DBMS de destino.

---
title: Transferencia de datos en su forma binaria ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 53531ff4a3b2e1441fabf22ec7a3ce12b15540eb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301417"
---
# <a name="transferring-data-in-its-binary-form"></a>Transferencia de datos en su forma binaria
Una aplicación puede transferir datos de forma segura (en la forma interna utilizada por un DBMS especificado) entre dos orígenes de datos que utilizan el mismo DBMS y la misma plataforma de hardware. Para un determinado fragmento de datos, los tipos de datos SQL deben ser los mismos en los orígenes de datos de origen y de destino. El tipo de datos C es SQL_C_BINARY.  
  
 Cuando la aplicación llama a **SQLFetch**, **SQLFetchScroll**o **SQLGetData** para recuperar los datos del origen de datos de origen, el controlador recupera los datos del origen de datos y los transfiere, sin conversión, a una ubicación de almacenamiento de tipo SQL_C_BINARY. Cuando la aplicación llama a **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPutData o SQLSetPos** para enviar los datos al origen de datos de destino, el controlador recupera los datos de la ubicación de almacenamiento y los transfiere, sin conversión, al origen de datos de destino.  
  
> [!NOTE]  
>  Las aplicaciones que transfieren datos (excepto datos binarios) de esta manera no son interoperables entre DBMS.  
  
 **SQLCopyDesc** se puede utilizar para copiar enlaces de fila desde el DBMS de origen a enlaces de parámetros en el DBMS de destino.

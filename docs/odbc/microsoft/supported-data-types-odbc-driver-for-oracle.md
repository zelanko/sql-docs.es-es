---
title: Tipos de datos admitidos (controlador ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: 21d5f8d9-a3aa-4aa4-bc37-ff8bc90c0870
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 313254a3a117984d666d7c7be7e506386ae34e3b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301120"
---
# <a name="supported-data-types-odbc-driver-for-oracle"></a>Tipos de datos admitidos (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC para Oracle admite todos los tipos de datos de Oracle 7,3; sin embargo, no es compatible con ninguno de los nuevos tipos de datos de Oracle8 que se enumeran aquí.  
  
|Tipo de datos|Oracle 7,3|Oracle8|  
|---------------|----------------|-------------|  
|BFILE|N/D|Incompatible|  
|BLOB|N/D|Incompatible|  
|CHAR|Compatible|Compatible|  
|CLOB|N/D|Incompatible|  
|DATE|Compatible|Compatible|  
|FLOAT|Compatible|Compatible|  
|INTEGER|Compatible|Compatible|  
|LONG|Compatible|Compatible|  
|LONG RAW|Compatible|Compatible|  
|NCHAR|N/D|Incompatible|  
|NCLOB|N/D|Incompatible|  
|NUMBER|Compatible|Compatible|  
|NVARCHAR2|N/D|Incompatible|  
|RAW|Compatible|Compatible|  
|VARCHAR2|Compatible|Compatible|  
|MLSLABEL|No se admite.|No se admite.|  
  
> [!NOTE]  
>  Para obtener más información sobre el tamaño permitido de la columna VARCHAR, vea [tamaño de columna VARCHAR](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) en esta guía.

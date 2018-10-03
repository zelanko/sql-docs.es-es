---
title: Subclave de controladores ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], drivers subkey
- registry entries for components [ODBC], drivers subkey
- drivers subkey [ODBC]
ms.assetid: 8edbf68f-d05d-4d77-92f6-e9500008f520
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 43be1c5e75998903ff4e64fc5f4230818a873ffc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772023"
---
# <a name="odbc-drivers-subkey"></a>Subclave de controladores de ODBC
Los valores bajo la subclave de controladores ODBC enumeran los controladores instalados. En la tabla siguiente se muestra el formato de estos valores.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|*Descripción del controlador*|REG_SZ|**instalado**|  
  
 El *descripción del controlador* nombre se define mediante el programador del controlador. Suele ser el nombre del DBMS asociado al controlador.  
  
 Por ejemplo, supongamos que se han instalado los controladores para los archivos de texto con formato y SQL Server. Los valores bajo la subclave de controladores ODBC podrían ser:  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```

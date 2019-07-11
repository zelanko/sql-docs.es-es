---
title: Asignación de SQLFreeConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLFreeConnect
- SQLFreeConnect function [ODBC], mapping
ms.assetid: 8a844538-93c0-4709-bab6-35c45e771d80
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b9a35275d95207fd8ceef296ecda4664a1c4e7f
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793603"
---
# <a name="sqlfreeconnect-mapping"></a>Asignación de SQLFreeConnect
Cuando una aplicación llama **SQLFreeConnect** a través de un ODBC *3.x* controlador, la llamada a  
  
```  
SQLFreeConnect(hdbc)   
```  
  
 se asigna a  
  
```  
SQLFreeHandle(SQL_HANDLE_DBC,Handle)  
```  
  
 con el *controlar* argumento establecido en el valor de *hdbc*.

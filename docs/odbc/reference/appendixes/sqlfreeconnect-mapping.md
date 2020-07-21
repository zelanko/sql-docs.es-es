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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20da205d53acbebca1fee12134c04f17fb8b2db3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302046"
---
# <a name="sqlfreeconnect-mapping"></a>Asignación de SQLFreeConnect
Cuando una aplicación llama a **SQLFreeConnect** a través de un controlador ODBC *3. x* , la llamada a  
  
```  
SQLFreeConnect(hdbc)   
```  
  
 está asignado a  
  
```  
SQLFreeHandle(SQL_HANDLE_DBC,Handle)  
```  
  
 con el argumento *Handle* establecido en el valor de *hdbc*.

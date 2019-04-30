---
title: Asignación de SQLAllocConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bdb63e9610d00c0736f640b6f4c4d743f3335c7d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280981"
---
# <a name="sqlallocconnect-mapping"></a>Asignación de SQLAllocConnect
Cuando una aplicación llama **SQLAllocConnect** a través de una aplicación ODBC 3. *x* controlador, la llamada a **SQLAllocConnect**(*henv*, *phdbc*) se asigna a **SQLAllocHandle** como sigue:  
  
1.  El Administrador de controladores se asigna una conexión y lo devuelve a la aplicación.  
  
2.  Cuando la aplicación establece una conexión, se llama el Administrador de controladores  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     en el controlador con *InputHandle* establecido en *henv*, y *OutputHandlePtr* establecido en *phdbc*.

---
title: "Asignación de SQLAllocConnect | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 001c430558b3db813bd316f3b4d913fe0eae26c2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlallocconnect-mapping"></a>Asignación de SQLAllocConnect
Cuando una aplicación llama **SQLAllocConnect** a través de una aplicación ODBC 3. *x* controlador, la llamada a **SQLAllocConnect**(*henv*, *phdbc*) se asigna a **SQLAllocHandle** como se indica a continuación:  
  
1.  El Administrador de controladores se asigna una conexión y se devuelve a la aplicación.  
  
2.  Cuando la aplicación establece una conexión, el Administrador de controladores llama  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     en el controlador con *InputHandle* establecido en *henv*, y *OutputHandlePtr* establecido en *phdbc*.

---
title: "Asignación de SQLAllocConnect | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0188c47d6abfd294dc1a9c20c04ea7d271443a18
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlallocconnect-mapping"></a>Asignación de SQLAllocConnect
Cuando una aplicación llama **SQLAllocConnect** a través de una aplicación ODBC 3.* x* controlador, la llamada a **SQLAllocConnect**(*henv*, *phdbc*) se asigna a **SQLAllocHandle** como se indica a continuación:  
  
1.  El Administrador de controladores se asigna una conexión y se devuelve a la aplicación.  
  
2.  Cuando la aplicación establece una conexión, el Administrador de controladores llama  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     en el controlador con *InputHandle* establecido en *henv*, y *OutputHandlePtr* establecido en *phdbc*.


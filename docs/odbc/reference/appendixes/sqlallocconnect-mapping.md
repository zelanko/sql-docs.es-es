---
title: SqlAllocConnect Mapping (Asignación de SQLAllocConnect) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25e72cd3830cea8504983f4348f6c200261490f4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305526"
---
# <a name="sqlallocconnect-mapping"></a>Asignación de SQLAllocConnect
Cuando una aplicación llama a **SQLAllocConnect** a través de un ODBC 3. *x* driver, la llamada a **SQLAllocConnect**(*henv*, *phdbc*) se asigna a **SQLAllocHandle** de la siguiente manera:  
  
1.  El Administrador de controladores asigna una conexión y la devuelve a la aplicación.  
  
2.  Cuando la aplicación establece una conexión, el Administrador de controladores llama  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     en el controlador con *InputHandle* establecido en *henv*, y *OutputHandlePtr* establecido en *phdbc*.

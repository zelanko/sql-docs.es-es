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
ms.openlocfilehash: 65c23f41ea9176c460c8fb32ece5e74dfb803541
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68065026"
---
# <a name="sqlallocconnect-mapping"></a>Asignación de SQLAllocConnect
Cuando una aplicación llama a **SQLAllocConnect** a través de ODBC 3. *x* , la llamada a **SQLAllocConnect**(*HENV*, *phdbc*) se asigna a **SQLAllocHandle** de la siguiente manera:  
  
1.  El administrador de controladores asigna una conexión y la devuelve a la aplicación.  
  
2.  Cuando la aplicación establece una conexión, el administrador de controladores llama a  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     en el controlador con *InputHandle* establecido en *HENV*y *OutputHandlePtr* establecido en *phdbc*.

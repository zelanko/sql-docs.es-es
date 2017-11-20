---
title: "Asignación de SQLAllocEnv | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLAllocEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocEnv
ms.assetid: 4bb51845-ee91-4b97-9dd4-2fab977f2aec
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 66261c8fd8236a4abc35ac70e29f63b49f646daf
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlallocenv-mapping"></a>Asignación de SQLAllocEnv
Cuando una aplicación llama **SQLAllocEnv** a través de una aplicación ODBC 3*.x* controlador, la llamada a **SQLAllocEnv**(*phenv*) se asigna a **SQLAllocHandle** como se indica a continuación:  
  
1.  El Administrador de controladores asigna un identificador de entorno y lo devuelve a la aplicación. Las llamadas del Administrador de controladores **SQLSetEnvAttr** para establecer el atributo de entorno SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC2.  
  
2.  Cuando la aplicación establece la primera conexión a un controlador, se llama el Administrador de controladores  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     en el controlador con *OutputHandlePtr* establecido en *phenv*.


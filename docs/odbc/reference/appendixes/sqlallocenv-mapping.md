---
title: Asignación de SQLAllocEnv | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLAllocEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocEnv
ms.assetid: 4bb51845-ee91-4b97-9dd4-2fab977f2aec
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 01618081862172fb951cfc21c0c7cc5675bb1062
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlallocenv-mapping"></a>Asignación de SQLAllocEnv
Cuando una aplicación llama **SQLAllocEnv** a través de una aplicación ODBC 3*.x* controlador, la llamada a **SQLAllocEnv**(*phenv*) se asigna a **SQLAllocHandle** como se indica a continuación:  
  
1.  El Administrador de controladores asigna un identificador de entorno y lo devuelve a la aplicación. Las llamadas del Administrador de controladores **SQLSetEnvAttr** para establecer el atributo de entorno SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC2.  
  
2.  Cuando la aplicación establece la primera conexión a un controlador, se llama el Administrador de controladores  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     en el controlador con *OutputHandlePtr* establecido en *phenv*.

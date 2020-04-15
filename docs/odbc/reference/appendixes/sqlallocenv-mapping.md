---
title: Asignación de SQLAllocEnv ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocEnv
ms.assetid: 4bb51845-ee91-4b97-9dd4-2fab977f2aec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb26e3443fabda2d6490c071b1f2668895e66b8d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304046"
---
# <a name="sqlallocenv-mapping"></a>Asignación de SQLAllocEnv
Cuando una aplicación llama a **SQLAllocEnv** a través de un controlador ODBC *3.x,* la llamada a **SQLAllocEnv**(*phenv*) se asigna a **SQLAllocHandle** de la siguiente manera:  
  
1.  El Administrador de controladores asigna un identificador de entorno y lo devuelve a la aplicación. El Administrador de controladores llama a **SQLSetEnvAttr** para establecer el atributo de entorno SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC2.  
  
2.  Cuando la aplicación establece la primera conexión con un controlador, el Administrador de controladores llama  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     en el controlador con *OutputHandlePtr* establecido *en phenv*.

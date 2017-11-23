---
title: "El programa de instalación de controlador DLL | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing ODBC components [ODBC], driver setup DLL
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: 49bab021-81fa-402e-b7a4-a5214f1fadc4
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9b7c64b6eed3a30a7c03d82f130e1dea8ca8e8bd
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="driver-setup-dll"></a>DLL de instalación de controlador
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo de Windows. Solo explícitamente debe instalar ODBC en versiones anteriores de Windows.  
  
 El programa de instalación de controlador DLL contiene la **ConfigDriver** y **ConfigDSN** funciones. **ConfigDriver** realiza las tareas de instalación específicos del controlador, por ejemplo, especificar la información específica del controlador en el registro. **ConfigDSN** mantiene información específica del controlador acerca de los orígenes de datos en el registro. Para obtener una descripción completa de estas funciones, vea [referencia de API de DLL de instalación](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 **ConfigDSN** llama a las funciones siguientes en el archivo DLL para mantener la información de origen de datos en el registro del programa de instalación:  
  
-   **SQLWriteDSNToIni**. Agregar un origen de datos.  
  
-   **SQLRemoveDSNFromIni**. Eliminar un origen de datos.  
  
-   **SQLWritePrivateProfileString**. Escribir un valor específico del controlador en una subclave de especificación del origen de datos.  
  
-   **SQLGetPrivateProfileString**. Leer un valor específico del controlador de una subclave de especificación del origen de datos.  
  
-   **SQLGetTranslator**. Pedir al usuario un nombre de traductor y una opción. Esta función llama a **ConfigTranslator** en el traductor de DLL de la instalación.  
  
 El programa de instalación de controlador archivo DLL está escrito por el programador del controlador. Puede ser parte del controlador del archivo DLL o un archivo DLL independiente.

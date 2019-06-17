---
title: DLL de instalación de controlador | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], driver setup DLL
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: 49bab021-81fa-402e-b7a4-a5214f1fadc4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 088c9b60861266bf99649343aec2e763097bf155
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63198193"
---
# <a name="driver-setup-dll"></a>DLL de instalación del controlador
> [!NOTE]  
>  Desde Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. ODBC explícitamente sólo debe instalar en versiones anteriores de Windows.  
  
 La configuración del controlador de archivo DLL contiene la **ConfigDriver** y **ConfigDSN** funciones. **ConfigDriver** lleva a cabo tareas de instalación específicos del controlador, como escribir la información específica del controlador en el registro. **ConfigDSN** mantiene información específica del controlador acerca de los orígenes de datos en el registro. Para obtener una descripción completa de estas funciones, vea [referencia de API de DLL de instalación](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 **ConfigDSN** llama a las funciones siguientes en el archivo DLL para mantener la información de origen de datos en el registro del instalador:  
  
-   **SQLWriteDSNToIni**. Agregar un origen de datos.  
  
-   **SQLRemoveDSNFromIni**. Eliminar un origen de datos.  
  
-   **SQLWritePrivateProfileString**. Escribir un valor específico del controlador en una subclave de especificación del origen de datos.  
  
-   **SQLGetPrivateProfileString**. Leer un valor específico del controlador de una subclave de especificación del origen de datos.  
  
-   **SQLGetTranslator**. Solicitar al usuario una opción y el nombre del traductor. Esta función llama a **ConfigTranslator** en el traductor de DLL de instalación.  
  
 La configuración del controlador de archivo DLL está escrito por el programador del controlador. Puede ser parte del controlador de archivo DLL o un archivo DLL independiente.

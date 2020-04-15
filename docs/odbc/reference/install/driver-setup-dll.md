---
title: DLL de configuración del controlador ( Driver Setup DLL) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0a2878591c92fe0b2070a295d9dc622c245c17e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306426"
---
# <a name="driver-setup-dll"></a>DLL de instalación del controlador
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. Solo debe instalar ODBC explícitamente en versiones anteriores de Windows.  
  
 El archivo DLL de instalación del controlador contiene las funciones **ConfigDriver** y **ConfigDSN.** **ConfigDriver** realiza tareas de instalación específicas del controlador, como escribir información específica del controlador en el registro. **ConfigDSN** mantiene información específica del controlador sobre los orígenes de datos en el registro. Para obtener una descripción completa de estas funciones, consulte Referencia de la [API de DLL](../../../odbc/reference/syntax/setup-dll-api-reference.md)de instalación .  
  
 **ConfigDSN** llama a las siguientes funciones en el archivo DLL del instalador para mantener la información del origen de datos en el registro:  
  
-   **SQLWriteDSNToIni**. Agregue un origen de datos.  
  
-   **SQLRemoveDSNFromIni**. Elimine un origen de datos.  
  
-   **SQLWritePrivateProfileString**. Escriba un valor específico del controlador en una subclave de especificación de origen de datos.  
  
-   **SQLGetPrivateProfileString**. Lea un valor específico del controlador de una subclave de especificación del origen de datos.  
  
-   **SQLGetTranslator**. Solicite al usuario un nombre y una opción de traductor. Esta función llama a **ConfigTranslator** en el archivo DLL de instalación del traductor.  
  
 El controlador DLL de instalación del controlador lo escribe el desarrollador del controlador. Puede ser parte de la DLL del controlador o un archivo DLL independiente.

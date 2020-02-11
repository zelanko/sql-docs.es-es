---
title: DLL de instalación del controlador | Microsoft Docs
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
ms.openlocfilehash: df91638f91091940e00e7a6a19d0fd6cb700f85f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094162"
---
# <a name="driver-setup-dll"></a>DLL de instalación del controlador
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. Solo debe instalar explícitamente ODBC en versiones anteriores de Windows.  
  
 El archivo DLL de instalación del controlador contiene las funciones **ConfigDriver** y **ConfigDSN** . **ConfigDriver** realiza tareas de instalación específicas del controlador, como la entrada de información específica del controlador en el registro. **ConfigDSN** mantiene información específica del controlador sobre los orígenes de datos en el registro. Para obtener una descripción completa de estas funciones, vea referencia de la [API de dll de configuración](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 **ConfigDSN** llama a las siguientes funciones en el archivo DLL del instalador para mantener la información del origen de datos en el registro:  
  
-   **SQLWriteDSNToIni**. Agregue un origen de datos.  
  
-   **SQLRemoveDSNFromIni**. Eliminar un origen de datos.  
  
-   **SQLWritePrivateProfileString**. Escriba un valor específico del controlador en una subclave de especificación de origen de datos.  
  
-   **SQLGetPrivateProfileString**. Leer un valor específico del controlador de una subclave de especificación de origen de datos.  
  
-   **SQLGetTranslator**. Pida al usuario un nombre y una opción de traductor. Esta función llama a **ConfigTranslator** en el archivo dll de instalación de Translator.  
  
 El archivo DLL de instalación del controlador está escrito por el desarrollador del controlador. Puede formar parte de la DLL del controlador o de un archivo DLL independiente.

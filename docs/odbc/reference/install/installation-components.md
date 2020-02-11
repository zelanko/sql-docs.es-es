---
title: Componentes de instalación | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
- ODBC [ODBC], component installation
ms.assetid: 9de15ca0-fe6a-4634-8709-a928d3c9cc73
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 34d1b6d143f6f40d73e2feeb0b718f3c3b3248fe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094130"
---
# <a name="installation-components"></a>Componentes de instalación
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. Solo debe instalar explícitamente ODBC en versiones anteriores de Windows.  
  
 El proceso de instalación se inicia cuando el usuario ejecuta el programa de instalación. El programa de instalación funciona junto con el *archivo DLL del instalador* y un *archivo dll de instalación del controlador* para cada controlador. Tanto el programa de instalación como el archivo DLL de instalación usan los argumentos de las funciones **SQLInstallDriverEx** y **SQLInstallTranslatorEx** para determinar qué archivos se deben copiar o eliminar para cada componente. En la ilustración siguiente se muestra la relación entre estos componentes de instalación.  
  
 ![Relación entre componentes de instalación](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]
>  El archivo ODBC. inf que se usó en ODBC *2. x* para describir los archivos requeridos por cada componente ODBC no se utiliza en ODBC *3. x*. No es necesario que los controladores que incluyen componentes de ODBC *3. x* creen un archivo ODBC. inf. La eliminación de **SQLInstallDriver** y **SQLInstallODBC**, y el desuso de **SQLInstallTranslator**, han representado ODBC. inf. La información del controlador que solía encontrarse en las secciones de la palabra clave driver de ODBC. inf se proporciona ahora en el argumento *lpszDriver* de **SQLInstallDriverEx**. La información de traductor que solía estar en las secciones [traductor ODBC] y especificación de traductor de ODBC. inf se proporciona ahora en el argumento *lpszTranslator* de **SQLInstallTranslatorEx**. Estos cambios permiten que el instalador de ODBC sea más portátil entre plataformas.  
  
 Para obtener más información acerca de estos componentes, consulte los temas siguientes al final de esta sección.  
  
-   [Programa de instalación](../../../odbc/reference/install/setup-program.md)  
  
-   [DLL instalador](../../../odbc/reference/install/installer-dll.md)  
  
-   [DLL de instalación del controlador](../../../odbc/reference/install/driver-setup-dll.md)

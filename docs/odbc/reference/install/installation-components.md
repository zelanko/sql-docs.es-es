---
title: Componentes de instalación ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0a196e9b935229fa03c6dd0eda92b8e99e69f0ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285255"
---
# <a name="installation-components"></a>Componentes de instalación
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. Solo debe instalar ODBC explícitamente en versiones anteriores de Windows.  
  
 El proceso de instalación se inicia cuando el usuario ejecuta el programa de instalación. El programa de instalación funciona junto con el *archivo DLL* del instalador y un archivo DLL de instalación del *controlador* para cada controlador. Tanto el programa de instalación como el archivo DLL del instalador utilizan los argumentos de las funciones **SQLInstallDriverEx** y **SQLInstallTranslatorEx** para determinar qué archivos copiar o eliminar para cada componente. En la ilustración siguiente se muestra la relación entre estos componentes de instalación.  
  
 ![Relación entre componentes de instalación](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]
>  El archivo Odbc.inf que se utilizó en ODBC *2.x* para describir los archivos requeridos por cada componente ODBC no se utiliza en ODBC *3.x*. Los controladores que envían componentes ODBC *3.x* no necesitan crear un archivo Odbc.inf. La eliminación de **SQLInstallDriver** y **SQLInstallODBC**, y el desuso de **SQLInstallTranslator**, han hecho innecesario odbc.inf. La información del controlador que solía estar en las secciones de palabra clave del controlador de Odbc.inf ahora se proporciona en el argumento *lpszDriver* en **SQLInstallDriverEx**. La información del traductor que solía estar en las secciones [ODBC Translator] y Translator Specification de Odbc.inf ahora se proporciona en el argumento *lpszTranslator* de **SQLInstallTranslatorEx**. Estos cambios permiten que el instalador ODBC sea más portátil entre plataformas.  
  
 Para obtener más información acerca de estos componentes, consulte los temas siguientes al final de esta sección.  
  
-   [Programa de instalación](../../../odbc/reference/install/setup-program.md)  
  
-   [DLL instalador](../../../odbc/reference/install/installer-dll.md)  
  
-   [DLL de instalación del controlador](../../../odbc/reference/install/driver-setup-dll.md)

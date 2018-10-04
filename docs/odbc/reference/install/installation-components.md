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
manager: craigg
ms.openlocfilehash: 961ff9fe552fa30eaad4667fdd1911a44f3a35f1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47793043"
---
# <a name="installation-components"></a>Componentes de instalación
> [!NOTE]  
>  Desde Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. ODBC explícitamente sólo debe instalar en versiones anteriores de Windows.  
  
 El proceso de instalación se inicia cuando el usuario ejecuta el programa de instalación. Funciona junto con el programa de instalación la *DLL instalador* y un *DLL de instalación de controlador* para cada controlador. El programa de instalación y el archivo DLL de instalador usan los argumentos de la **SQLInstallDriverEx** y **SQLInstallTranslatorEx** funciones para determinar qué archivos desea copiar o eliminar para cada componente. La siguiente ilustración muestra la relación entre estos componentes de instalación.  
  
 ![Relación entre componentes de instalación](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]  
>  El archivo de ODBC se usó en ODBC 2. *x* para describir los archivos requeridos por cada ODBC el componente no se usa en ODBC 3 *.x*. Los controladores que se incluyen ODBC 3 *.x* no es necesario crear un archivo de ODBC los componentes. La eliminación de **SQLInstallDriver** y **SQLInstallODBC**y el desuso de **SQLInstallTranslator**, impiden que ODBC innecesarios. La información del controlador que solía haber en las secciones de la palabra clave Driver de ODBC ahora se proporciona en el *lpszDriver* argumento en **SQLInstallDriverEx**. La información de traductor que solía haber en el [ODBC traductor] y secciones de la especificación del traductor de ODBC ahora se proporciona en el *lpszTranslator* argumento de **SQLInstallTranslatorEx**. Estos cambios permiten que el instalador de ODBC para que sea más portátil entre plataformas.  
  
 Para obtener más información acerca de estos componentes, vea los temas siguientes al final de esta sección.  
  
-   [Programa de instalación](../../../odbc/reference/install/setup-program.md)  
  
-   [DLL instalador](../../../odbc/reference/install/installer-dll.md)  
  
-   [DLL de instalación del controlador](../../../odbc/reference/install/driver-setup-dll.md)

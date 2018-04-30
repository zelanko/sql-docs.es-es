---
title: Instalación de versiones de idioma de SQL Server Management Studio (SSMS) distintas del inglés | Microsoft Docs
description: Instalación de versiones de idioma de SQL Server Management Studio (SSMS) distintas del inglés
ms.custom: ''
ms.date: 12/08/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 336b26d502d6cb40ab7c3be5de35d52f3d019b8a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="install-non-english-language-versions-of-sql-server-management-studio-ssms"></a>Instalación de versiones de idioma de SQL Server Management Studio (SSMS) distintas del inglés 

[SSMS está disponible en varios idiomas](download-sql-server-management-studio-ssms.md#available-languages), pero el programa de instalación de SSMS bloquea la instalación en equipos en los que la configuración regional del sistema no coincide con el idioma de SSMS. 

Las instrucciones siguientes varían según la versión de Windows. Estas son para Windows 10.

## <a name="install-non-english-ssms-on-a-computer-running-an-english-operating-system-os"></a>Instalación de SSMS en un idioma distinto del inglés en un equipo que ejecuta un sistema operativo (SO) en inglés

1. Instale el paquete de idioma de Windows correspondiente al idioma que quiere que se use en SSMS: 
   - **Configuración** > **Hora e idioma** > **Región y idioma** > **Agregar un idioma** 
2. A continuación, establezca la configuración regional para usar el paquete de idioma instalado en el paso anterior; para ello, haga clic en el idioma que acaba de instalar y seleccione **Establecer como predeterminado**. (Después de instalar SSMS, puede devolver la configuración regional a inglés).
3. Una vez que el sistema operativo se ejecuta en el idioma deseado, [instale la versión de SSMS de ese mismo idioma](download-sql-server-management-studio-ssms.md#available-languages). La primera vez que instale un nuevo idioma de SSMS, use el paquete completo. En las posteriores instalaciones, puede usar el paquete de actualización.
4. Ejecute SSMS. Debería mostrarse en el idioma instalado en el paso anterior.
5. Devuelva otra vez la configuración regional del equipo a inglés.

## <a name="install-ssms-in-a-language-other-than-the-language-of-the-installed-os"></a>Instalación de SSMS en un idioma distinto al del sistema operativo instalado

1. Instale el paquete de idioma de Windows correspondiente al idioma que quiere que se use en SSMS: 
   - **Configuración** > **Hora e idioma** > **Región y idioma** > **Agregar un idioma** 
2. A continuación, establezca la configuración regional para usar el paquete de idioma instalado en el paso anterior; para ello, haga clic en el idioma que acaba de instalar y seleccione **Establecer como predeterminado**. 
3. Una vez que el sistema operativo se ejecuta en el idioma deseado, [instale la versión de SSMS de ese mismo idioma](download-sql-server-management-studio-ssms.md#available-languages). La primera vez que instale un nuevo idioma de SSMS, use el paquete completo. En las posteriores instalaciones, puede usar el paquete de actualización.
4. Para cada idioma que desee instalar que no coincida con el idioma de la primera versión de SSMS que se ha instalado, instale el paquete de idioma correspondiente de Visual Studio 2015 Shell (aislado):
   - Vaya a [https://connect.microsoft.com/VisualStudio/ExtendVS](https://connect.microsoft.com/VisualStudio/ExtendVS) (es posible que tenga que iniciar sesión y completar el proceso *Registro en Connect*).
   - Descargue el paquete de idioma deseado de Visual Studio 2015 Shell (aislado) e instálelo.

   > [!IMPORTANT]
   > Use los pasos anteriores para instalar el paquete de idioma de Visual Studio 2015 aislado; no use el vínculo **Obtener idiomas adicionales** en **Herramientas** | **Opciones** | **Configuración internacional**. 

5. Ejecute SSMS y seleccione el idioma con el que quiere usarlo:
   - **Herramientas** | **Opciones** | **Configuración**
1. Cierre y reinicie SSMS.

## <a name="next-steps"></a>Pasos siguientes

- [Tutorial: SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/tutorials/tutorial-sql-server-management-studio)
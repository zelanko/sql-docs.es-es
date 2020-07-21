---
title: 'Paso 1: Configuración del entorno de pymssql'
description: El paso 1 de esta guía de introducción implica la instalación de Python, Microsoft ODBC Driver for SQL Server y pymssql en el entorno de desarrollo.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d5eb4a746cf8847c8300091677fe4e07e8173707
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634615"
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>Paso 1: Configuración del entorno de desarrollo para el desarrollo de Python pymssql
Tendrá que configurar el entorno de desarrollo con los requisitos previos para desarrollar una aplicación con el controlador de Python para SQL Server.    
  
Los controladores de SQL para Python usan el protocolo TDS, que está habilitado de forma predeterminada en SQL Server y Azure SQL Database.  No se requiere ninguna configuración adicional.  
  
## <a name="windows"></a>Windows  
  
1. **Instale el entorno de ejecución de Python y el administrador de paquetes de PIP**.  
a. Vaya a [python.org](https://www.python.org/downloads/).  
b. Haga clic en el vínculo del archivo MSI adecuado de Windows Installer.   
c. Una vez descargado, ejecute el archivo msi para instalar el entorno de ejecución de Python.  
  
2. **Descargar el del módulo pymssql** desde [aquí](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)  
  
    Asegúrese de elegir el archivo `whl` correcto.  Por ejemplo: Si usa Python 2.7 en un equipo de 64 bits, elija `pymssql‑2.1.1‑cp27‑none‑win_amd64.whl`. Una vez descargado el archivo `whl`, colóquelo en la carpeta C:\Python27.  
      
3. **Abra cmd.exe**.  
  
4. **Instale el módulo pymssql**.  
    Por ejemplo, si usa Python 2.7 en un equipo de 64 bits:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Instale el entorno de ejecución de Python y el administrador de paquetes de PIP**.  Python viene preinstalado en la mayoría de las distribuciones de Ubuntu.  Si el equipo no tiene Python instalado, puede descargar el tarball de origen desde [python.org](https://www.python.org/downloads/) y compilar localmente, o puede usar el administrador de paquetes:  
```  
> sudo apt-get install python   
```  
  
2.  **Abra el terminal**.  
  
3.  **Instalar el módulo pymssql y las dependencias**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="macos"></a>macOS
  
1. **Instalar el entorno de ejecución de Python y del administrador de paquetes de PIP**  
a. Vaya a [python.org](https://www.python.org/downloads/).  
b. Haga clic en el vínculo pkg del instalador de macOS adecuado.   
c. Una vez descargado, ejecute el archivo pkg para instalar el entorno de ejecución de Python.  
  
2.  **Abrir terminal**  
  
3. **Instalar el administrador de paquetes de Homebrew**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
4.  **Instalar el módulo FreeTDS**  
```  
> brew install FreeTDS  
```  
  
5.  **Instalar el módulo pymssql**  
```  
> sudo -H pip install pymssql  
```

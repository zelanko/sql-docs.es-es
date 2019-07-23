---
title: 'Paso 1: configurar el entorno de desarrollo de pymssql Python | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5bf2942b79cf7e72efbb36a53019de8208cd3b8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935824"
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>Paso 1: configurar el entorno de desarrollo para el desarrollo de Python pymssql
Tendrá que configurar el entorno de desarrollo con los requisitos previos para desarrollar una aplicación con el controlador de Python para SQL Server.    
  
Tenga en cuenta que los controladores de SQL de Python usan el protocolo TDS, que está habilitado de forma predeterminada en SQL Server y Azure SQL Database.  No se requiere ninguna configuración adicional.  
  
## <a name="windows"></a>Windows  
  
1. **Instalación del tiempo de ejecución de Python y del administrador de paquetes de PIP**  
A. Vaya a [Python.org](https://www.python.org/downloads/)  
B. Haga clic en el vínculo MSI de Windows Installer adecuado.   
c. Una vez descargado, ejecute el archivo MSI para instalar el tiempo de ejecución de Python  
  
2. **Descargar el módulo pymssql** desde [aquí](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)  
  
    Asegúrese de elegir el archivo WHL correcto.  Por ejemplo: Si usa Python 2,7 en un equipo de 64 bits, elija: pymssql-2.1.1-cp27-None-win_amd64. WHL. Una vez que descargue el archivo. WHL, colóquelo en la carpeta C:/Python27  
      
3. **Abra cmd. exe**  
  
4. **Instalación del módulo pymssql**     
    Por ejemplo, si usa Python 2,7 en un equipo de 64 bits:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Instalación del tiempo de ejecución de Python y del administrador de paquetes de PIP**  Python viene preinstalado en la mayoría de las distribuciones de Ubuntu.  Si el equipo no tiene Python instalado, puede descargar el tarball de origen de [Python.org](https://www.python.org/downloads/) y compilar localmente, o bien puede usar el administrador de paquetes:  
```  
> sudo apt-get install python   
```  
  
2.  **Abrir terminal**  
  
3.  **Instalación del módulo pymssql y las dependencias**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="mac"></a>Mac  
  
1. **Instalación del tiempo de ejecución de Python y del administrador de paquetes de PIP**  
A. Vaya a [Python.org](https://www.python.org/downloads/)  
B. Haga clic en el vínculo paquete de Mac Installer adecuado.   
c. Una vez descargado, ejecute el paquete para instalar el tiempo de ejecución de Python  
  
2.  **Abrir terminal**  
  
3. **Instalación del administrador de paquetes de homebrew**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
4.  **Instalación del módulo FreeTDS**  
```  
> brew install FreeTDS  
```  
  
5.  **Instalación del módulo pymssql**  
```  
> sudo -H pip install pymssql  
```

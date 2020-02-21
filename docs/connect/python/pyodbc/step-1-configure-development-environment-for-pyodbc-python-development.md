---
title: 'Paso 1: Configuración del entorno de desarrollo de Python pyodbc | Microsoft Docs'
ms.custom: ''
ms.date: 07/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a1a43540d866faaf79b1c020eb255689862e6d97
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67992519"
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>Paso 1: Configuración del entorno de desarrollo para el desarrollo de Python pyodbc

## <a name="windows"></a>Windows  
Conexión a SQL Database mediante Python - pyodbc en Windows:
  
1. **Descargue el instalador de Python**.  
  Si la máquina no tiene Python, instálelo. Vaya a la [página de descarga de Python](https://www.python.org/downloads/windows/) y descargue el instalador adecuado. Por ejemplo, si está en una máquina de 64 bits, descargue el instalador de Python 2.7 o 3.7 (x64).  
  
2. **Instale Python**.  Una vez descargado el instalador, realice los pasos siguientes: a. Haga doble clic en el archivo para iniciar el instalador. b. Seleccione su idioma y acepte los términos. c. Siga las instrucciones que aparecen en pantalla y Python debería instalarse en el equipo. d. Para comprobar que Python está instalado, vaya a `C:\Python27` o `C:\Python37` y ejecute `python -V` o `py -V` (para 3.x). 
      
3. [**Instale Microsoft ODBC Driver for SQL Server en Windows**](../../odbc/windows/system-requirements-installation-and-driver-files.md#installing-microsoft-odbc-driver-for-sql-server)
  
4. **Abra cmd.exe como administrador**.     

5. **Instale pyodbc con el administrador de paquetes de pip - Python** (reemplace `C:\Python27\Scripts` por la ruta de acceso de Python instalada).
```  
> cd C:\Python27\Scripts  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
Conexión a SQL Database mediante Python - pyodbc:
  
1. **Abra el terminal**.  

2. [**Instale Microsoft ODBC Driver for SQL Server en Linux**](../../odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

3.  **Instale pyodbc**.  
```  
> sudo -H pip install pyodbc
```

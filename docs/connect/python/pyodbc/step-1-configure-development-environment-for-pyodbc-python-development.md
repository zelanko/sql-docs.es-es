---
title: 'Paso 1: configurar el entorno de desarrollo de pyodbc Python | Microsoft Docs'
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992519"
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>Paso 1: Configurar el entorno de desarrollo para el desarrollo de Python pyodbc

## <a name="windows"></a>Windows  
Conéctese a SQL Database mediante Python-pyodbc en Windows:
  
1. **Descargue el instalador de Python**.  
  Si el equipo no tiene Python, instálelo. Vaya a la [Página de descarga de Python](https://www.python.org/downloads/windows/) y descargue el instalador adecuado. Por ejemplo, si está en un equipo de 64 bits, descargue el instalador de Python 2,7 o 3,7 (x64).  
  
2. **Instale Python**.  Una vez descargado el instalador, realice los pasos siguientes: a. Haga doble clic en el archivo para iniciar el instalador. B. Seleccione su idioma y acepte los términos. c. Siga las instrucciones que aparecen en pantalla y Python debe estar instalado en el equipo. d. Para comprobar que Python está instalado, vaya `C:\Python27` a o `C:\Python37` y ejecute `python -V` o `py -V` (para 3. x). 
      
3. [**Instale Microsoft ODBC Driver for SQL Server en Windows**](../../odbc/windows/system-requirements-installation-and-driver-files.md#installing-microsoft-odbc-driver-for-sql-server)
  
4. **Abra cmd. exe como administrador.**     

5. **Instalación de pyodbc con el administrador de paquetes de PIP-Python** (Reemplace `C:\Python27\Scripts` por la ruta de acceso de Python instalada)
```  
> cd C:\Python27\Scripts  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
Conéctese a SQL Database mediante Python-pyodbc:
  
1. **Abrir terminal**  

2. [**Instale Microsoft ODBC Driver for SQL Server en Linux**](../../odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

3.  **Instalación de pyodbc**  
```  
> sudo -H pip install pyodbc
```

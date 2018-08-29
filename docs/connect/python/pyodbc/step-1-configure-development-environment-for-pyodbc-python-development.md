---
title: 'Paso 1: Configurar el entorno de desarrollo de Python pyodbc | Microsoft Docs'
ms.custom: ''
ms.date: 07/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f588174ea80677066628cb3e756d7c38bd42fba
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2018
ms.locfileid: "42784322"
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>Paso 1: Configurar el entorno de desarrollo para el desarrollo de Python pyodbc

## <a name="windows"></a>Windows  
Conexión a SQL Database mediante Python - pyodbc en Windows:
  
1. **Descargue el instalador de Python**.  
  Si el equipo no tiene Python, instálelo. Vaya a la [página de descarga de Python](https://www.python.org/downloads/windows/) y descargue los instaladores adecuados. Por ejemplo, si se encuentra en un equipo de 64 bits, descargue al instalador de Python 2.7 o 3.7 (x 64).  
  
2. **Instale Python**.  Una vez descargado el instalador, realice los pasos siguientes: una. Haga doble clic en el archivo para iniciar al instalador. B. Seleccione su idioma y acepte los términos. c. Siga las instrucciones en pantalla y Python debe instalarse en el equipo. d. Puede comprobar que está instalado Python, vaya a `C:\Python27` o `C:\Python37` y ejecute `python -V` o `py -V` (para 3.x) 
      
3. [**Instale Microsoft ODBC Driver for SQL Server en Windows**](../../odbc/windows/system-requirements-installation-and-driver-files.md#installing-microsoft-odbc-driver-for-sql-server)
  
4. **Abra cmd.exe como administrador**     

5. **Instale pyodbc con pip - Administrador de paquetes de Python** (reemplace `C:\Python27\Scripts` con la ruta de acceso de Python instalada)
```  
> cd C:\Python27\Scripts  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
Conexión a SQL Database mediante Python - pyodbc:
  
1. **Abrir terminal**  

2. [**Instale Microsoft ODBC Driver for SQL Server en Linux**](../../odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

3.  **Instale pyodbc**  
```  
> sudo -H pip install pyodbc
```

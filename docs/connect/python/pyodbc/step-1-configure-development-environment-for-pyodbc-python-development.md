---
title: 'Paso 1: Configurar el entorno de desarrollo de Python pyodbc | Documentos de Microsoft'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: python
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: 64ce99a11d0942efaaaee2ba70831cd0f5e6b236
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>Paso 1: Configurar el entorno de desarrollo para pyodbc desarrollo Python

## <a name="windows"></a>Windows  
Conectarse a la base de datos SQL mediante el uso de Python - pyodbc en Windows:
  
1. **Descargue el instalador de Python**  
  Si su equipo no tiene Python debe instalarlo. Vaya el [página de descarga de Python](https://www.python.org/downloads/windows/) y descargue los instaladores adecuados. Por ejemplo, si se encuentra en un equipo de 64 bits, descargar el instalador de Python 2.7 o 3.5 (x 64).  
  
2. **Instalar Python** una vez descargado el programa de instalación, haga lo siguiente: una. Haga doble clic en el archivo para iniciar el programa de instalación. B. Seleccione su idioma y acepte los términos. c. Siga las instrucciones que aparecen en la pantalla y Python debe instalarse en el equipo. d. Puede comprobar que es Python está instalado, vaya a C:\Python27 o C:\Python35 y ejecutar python - v o copiar - v (de 3.x) 
      
3. [**Instalar al controlador ODBC de Microsoft**](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)
  
4. **Abra cmd.exe como administrador**     

5. **Instalar pyodbc con pip: el Administrador de paquetes de Python**
```  
> cd C:\Python27\Scripts>  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
Conectarse a la base de datos SQL mediante el uso de Python - pyodbc en Ubuntu y RedHat:
  
1. **Abra terminal**  

2. **Instale Microsoft ODBC Driver 13 para Linux** para Ubuntu 15.04 + 
``` 
> sudo su  
> wget https://gallery.technet.microsoft.com/ODBC-Driver-13-for-Ubuntu-b87369f0/file/154097/2/installodbc.sh  
> sh installodbc.sh  
```   

  Para RedHat 6,7 
``` 
> sudo su 
> wget https://gallery.technet.microsoft.com/ODBC-Driver-13-for-SQL-8d067754/file/153653/4/install.sh 
> sh install.sh 
```  
  
3.  **Instalar pyodbc**  
```  
> sudo -H pip install pyodbc
```
